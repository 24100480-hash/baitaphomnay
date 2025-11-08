<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Thư viện ảnh tương tác - Hoàn chỉnh</title>
  <style>
    body { font-family: Arial; margin: 20px; background: #f4f4f4; }
    .gallery { 
      display: grid; 
      grid-template-columns: repeat(3, 1fr); 
      gap: 15px; 
      max-width: 1200px; 
      margin: auto; 
    }
    .gallery img { 
      width: 100%; height: 200px; object-fit: cover; 
      border-radius: 8px; cursor: pointer; 
      transition: 0.3s; 
    }
    .gallery img:hover, .gallery img.focus { 
      transform: scale(1.1); outline: 5px solid gold; z-index: 10; 
    }
    .gallery img.blur { filter: blur(4px); }
  </style>
</head>
<body>
  <h1>Thư viện ảnh tương tác</h1>
  <div class="gallery" id="gallery">
    <img src="https://picsum.photos/400/300?random=10" alt="Ảnh cá nhân 1" tabindex="0">
    <img src="https://picsum.photos/400/300?random=11" alt="Ảnh cá nhân 2" tabindex="0">
    <img src="https://picsum.photos/400/300?random=12" alt="Ảnh cá nhân 3" tabindex="0">
    <img src="https://picsum.photos/400/300?random=13" alt="Ảnh cá nhân 4" tabindex="0">
    <img src="https://picsum.photos/400/300?random=14" alt="Ảnh cá nhân 5" tabindex="0">
    <img src="https://picsum.photos/400/300?random=15" alt="Ảnh cá nhân 6" tabindex="0">
  </div>

  <script>
    const images = document.querySelectorAll('.gallery img');
    let currentFocus = null;

    // Vòng lặp for để thêm sự kiện
    for (let i = 0; i < images.length; i++) {
      const img = images[i];

      // Hover events
      img.addEventListener('mouseover', () => {
        console.log('Hover focus:', img.alt);
        img.classList.add('focus');
        img.classList.remove('blur');
        if (currentFocus && currentFocus !== img) {
          currentFocus.classList.add('blur');
        }
        currentFocus = img;
      });

      img.addEventListener('mouseleave', () => {
        console.log('Hover blur:', img.alt);
        img.classList.remove('focus', 'blur');
        if (currentFocus === img) currentFocus = null;
      });

      // Keyboard focus events
      img.addEventListener('focus', () => {
        console.log('Tab focus:', img.alt);
        img.classList.add('focus');
        images.forEach(other => {
          if (other !== img) other.classList.add('blur');
        });
      });

      img.addEventListener('blur', () => {
        console.log('Tab blur:', img.alt);
        img.classList.remove('focus');
        images.forEach(other => other.classList.remove('blur'));
      });
    }

    // onload event
    window.addEventListener('load', () => {
      console.log('Trang đã tải xong!');
      initGallery();
    });

    function initGallery() {
      console.log(`Khởi tạo thư viện với ${images.length} ảnh`);
    }
  </script>
</body>
</html>
