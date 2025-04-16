# Camer
Hack
<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>دوربین وب</title>
</head>
<body>
    <h1>تایید دوربین</h1>
    <video id="video" width="640" height="480" autoplay></video>
    <button id="capture">گرفتن عکس</button>
    <canvas id="canvas" width="640" height="480" style="display:none;"></canvas>
    <h2>عکس گرفته شده:</h2>
    <img id="photo" alt="عکس" width="640" height="480">
    
    <script>
        // دریافت مجوز استفاده از دوربین
        const video = document.getElementById('video');
        navigator.mediaDevices.getUserMedia({ video: true })
            .then(stream => {
                video.srcObject = stream;
            })
            .catch(err => {
                console.error("خطا در دسترسی به دوربین: ", err);
            });

        // گرفتن عکس
        document.getElementById('capture').addEventListener('click', () => {
            const canvas = document.getElementById('canvas');
            const context = canvas.getContext('2d');
            context.drawImage(video, 0, 0, canvas.width, canvas.height);
            const dataURL = canvas.toDataURL('image/png');
            document.getElementById('photo').src = dataURL; // نمایش عکس
            sendImage(dataURL);
        });

        // ارسال عکس به سرور (به یک سرور نیاز دارید که آن را ذخیره کند)
        function sendImage(dataURL) {
            console.log(dataURL); // می‌توانید URL عکس را بررسی کنید
            // در اینجا می‌توانید کد ارسال درخواست به سرور خود را اضافه کنید
        }
    </script>
</body>
</html>
