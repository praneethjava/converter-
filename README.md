# converter-
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JPG to PNG & PNG to JPG Converter</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background: #fff;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            text-align: center;
            max-width: 400px;
            width: 100%;
        }
        h2 {
            margin-bottom: 20px;
            color: #333;
        }
        input[type="file"] {
            margin-bottom: 20px;
            width: 100%;
        }
        select {
            padding: 10px;
            width: 100%;
            margin-bottom: 20px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        button {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            width: 100%;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #0056b3;
        }
        #downloadArea {
            margin-top: 20px;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Image Converter</h2>
    <input type="file" id="uploadImage" accept="image/jpeg, image/png">
    
    <select id="formatSelect">
        <option value="image/png">Convert to PNG</option>
        <option value="image/jpeg">Convert to JPG</option>
    </select>
    
    <button onclick="convertImage()">Convert & Download</button>
    
    <div id="downloadArea"></div>
</div>

<script>
    function convertImage() {
        const fileInput = document.getElementById('uploadImage');
        const formatSelect = document.getElementById('formatSelect').value;
        const downloadArea = document.getElementById('downloadArea');
        
        if (fileInput.files.length === 0) {
            alert("කරුණාකර පළමුව පින්තූරයක් තෝරන්න!");
            return;
        }

        const file = fileInput.files[0];
        const reader = new FileReader();

        reader.onload = function(event) {
            const img = new Image();
            img.src = event.target.result;

            img.onload = function() {
                const canvas = document.createElement('canvas');
                canvas.width = img.width;
                canvas.height = img.height;

                const ctx = canvas.getContext('2d');
                ctx.drawImage(img, 0, 0);

                const dataUrl = canvas.toDataURL(formatSelect);
                
                const extension = formatSelect === 'image/png' ? 'png' : 'jpg';
                const downloadLink = document.createElement('a');
                downloadLink.href = dataUrl;
                downloadLink.download = `converted-image.${extension}`;
                downloadLink.innerText = `Download Converted Image (${extension.toUpperCase()})`;
                downloadLink.style.display = 'inline-block';
                downloadLink.style.marginTop = '15px';
                downloadLink.style.color = '#28a745';
                downloadLink.style.fontWeight = 'bold';
                downloadLink.style.textDecoration = 'none';

                downloadArea.innerHTML = '';
                downloadArea.appendChild(downloadLink);
            }
        }

        reader.readAsDataURL(file);
    }
</script>

</body>
</html>
