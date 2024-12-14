![Screenshot 2024-12-12 223814](https://github.com/user-attachments/assets/51c4d0d3-1a1f-4307-a553-8e8edd59f82f)# Ex.08 Design of Interactive Image Gallery
# Date:
10/12/24
# AIM:
To design a web application for an inteactive image gallery with minimum five images.

# DESIGN STEPS:
## Step 1:
Clone the github repository and create Django admin interface.

## Step 2:
Change settings.py file to allow request from all hosts.

## Step 3:
Use CSS for positioning and styling.

## Step 4:
Write JavaScript program for implementing interactivity.

## Step 5:
Validate the HTML and CSS code.

## Step 6:
Publish the website in the given URL.

# PROGRAM :
imagegallery.html

~~~

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Photo Gallery</title>
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            background: linear-gradient(to bottom, #e3f2fd, #bbdefb);
            color: #333;
        }

        header {
            background: linear-gradient(90deg, #2196f3, #6a1b9a);
            color: #fff;
            width: 100%;
            padding: 1.5rem;
            text-align: center;
            font-size: 2rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            font-weight: bold;
        }

        .gallery-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 20px;
            padding: 30px;
        }

        .photo {
            position: relative;
            width: 250px;
            height: 250px;
            overflow: hidden;
            border-radius: 15px;
            cursor: pointer;
            box-shadow: 0 6px 10px rgba(0, 0, 0, 0.15);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            background: #f1f8e9;
            opacity: 0;
            transform: translateY(30px);
            animation: fadeIn 0.5s ease forwards;
        }

        @keyframes fadeIn {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .photo:nth-child(odd) {
            animation-delay: 0.2s;
        }

        .photo:nth-child(even) {
            animation-delay: 0.4s;
        }

        .photo:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 20px rgba(0, 0, 0, 0.2);
        }

        .photo img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.3s ease;
        }

        .photo:hover img {
            transform: scale(1.2);
        }

        .photo-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.6);
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            opacity: 0;
            transition: opacity 0.3s ease;
            font-size: 1.2rem;
            font-weight: 500;
        }

        .photo:hover .photo-overlay {
            opacity: 1;
        }

        #lightbox {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(33, 33, 33, 0.95);
            display: flex;
            justify-content: center;
            align-items: center;
            visibility: hidden;
            opacity: 0;
            transition: opacity 0.3s ease, visibility 0.3s ease;
        }

        #lightbox img {
            max-width: 85%;
            max-height: 85%;
            border-radius: 10px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.4);
        }

        #lightbox.visible {
            visibility: visible;
            opacity: 1;
        }

        #lightbox .close {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 2rem;
            color: white;
            cursor: pointer;
            background: rgba(33, 33, 33, 0.8);
            border-radius: 50%;
            width: 40px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: background 0.3s ease;
        }

        #lightbox .close:hover {
            background: rgba(255, 255, 255, 0.4);
        }

        #lightbox .navigation {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            font-size: 2rem;
            color: white;
            cursor: pointer;
            background: rgba(33, 33, 33, 0.8);
            border-radius: 50%;
            width: 50px;
            height: 50px;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: background 0.3s ease;
        }

        #lightbox .navigation:hover {
            background: rgba(255, 255, 255, 0.4);
        }

        #lightbox .prev {
            left: 20px;
        }

        #lightbox .next {
            right: 20px;
        }
    </style>
</head>
<body>
    <header>Interactive Photo Gallery</header>

    <div class="gallery-container" id="gallery-container">
        <!-- Images will be loaded dynamically -->
    </div>

    <div id="lightbox">
        <span class="close" onclick="closeLightbox()">&times;</span>
        <span class="navigation prev" onclick="showPrevious()">&#10094;</span>
        <span class="navigation next" onclick="showNext()">&#10095;</span>
        <img id="lightbox-img" src="" alt="">
    </div>

    <script>
        const images = [
            { src: 'https://img.etimg.com/thumb/width-420,height-315,imgsize-402366,resizemode-75,msid-115654914/news/sports/india-vs-australia-test-series-yashasvi-jaiswal-virat-kohli-push-lead-past-400-as-india-reach-359-5-at-tea-in-perth/perth-australia-nov-23-ani-indias-yashasvi-jaiswal-celebrates-his-maiden-.jpg', title: 'Photo 1' },
            { src: 'https://images.indianexpress.com/2024/11/IND-AUS-42.jpg', title: 'Photo 2' },
            { src: 'https://library.sportingnews.com/styles/crop_style_16_9_desktop/s3/2024-11/GettyImages-2186729290.jpg?h=fa7386d1&itok=KVStcur2', title: 'Photo 3' },
            { src: 'https://images.mykhel.com/img/2024/11/pant-jurel-ind-vs-nz1-1730697560.jpg', title: 'Photo 4' },
            { src: 'https://static.cricketaddictor.com/images/posts/2024/FotoJet-7--40.webp?q=80', title: 'Photo 5' },
            { src: 'https://static.toiimg.com/thumb/msid-97725973,width-400,resizemode-4/97725973.jpg', title: 'Photo 6' },
            { src: 'https://img1.hscicdn.com/image/upload/f_auto/lsci/db/PICTURES/CMS/315100/315122.6.jpg', title: 'Photo 7' },
            { src: 'https://c.ndtvimg.com/2023-03/3r4pqs98_nathan-lyon-bcci_625x300_02_March_23.jpg?im=FaceCrop,algorithm=dnn,width=806,height=605', title: 'Photo 8' },
            { src: 'https://www.hindustantimes.com/ht-img/img/2024/12/06/1000x563/CRICKET-AUS-IND-63_1733485859017_1733485893519.jpg', title: 'Photo 9' },
            { src: 'https://c.ndtvimg.com/2024-12/b8g632e8_india-australia-afp_625x300_07_December_24.jpeg?im=FeatureCrop,algorithm=dnn,width=806,height=605', title: 'Photo 10' }
        ];

        const galleryContainer = document.getElementById('gallery-container');

        images.forEach((image, index) => {
            const photoDiv = document.createElement('div');
            photoDiv.className = 'photo';
            photoDiv.innerHTML = `
                <img src="${image.src}" alt="${image.title}">
                <div class="photo-overlay">${image.title}</div>
            `;
            photoDiv.onclick = () => openLightbox(index);
            galleryContainer.appendChild(photoDiv);
        });

        let currentIndex = 0;

        function openLightbox(index) {
            currentIndex = index;
            const lightbox = document.getElementById('lightbox');
            const lightboxImg = document.getElementById('lightbox-img');
            lightboxImg.src = images[currentIndex].src;
            lightbox.classList.add('visible');
        }

        function closeLightbox() {
            const lightbox = document.getElementById('lightbox');
            lightbox.classList.remove('visible');
        }

        function showPrevious() {
            currentIndex = (currentIndex - 1 + images.length) % images.length;
            document.getElementById('lightbox-img').src = images[currentIndex].src;
        }

        function showNext() {
            currentIndex = (currentIndex + 1) % images.length;
            document.getElementById('lightbox-img').src = images[currentIndex].src;
        }
    </script>
</body>
</html>
~~~
views.py
~~~
def gallery(request):
    return render(request,"imagegallery.html")
~~~
urls.py
~~~
from django.contrib import admin
from django.urls import path
from myapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('gallery/',views.gallery)
]
~~~
# OUTPUT:
![Screenshot 2024-12-12 223814](https://github.com/user-attachments/assets/29f5552f-6ff4-4b6d-9751-fa15edd5d349)

![Screenshot 2024-12-13 102708](https://github.com/user-attachments/assets/39b19f4f-fda3-422b-a172-da03a4746728)

![Screenshot 2024-12-13 102802](https://github.com/user-attachments/assets/8a212353-751e-4188-b7a3-1e8dff4b307b)

# RESULT:
The program for designing an interactive image gallery using HTML, CSS and JavaScript is executed successfully.
