<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>File to PDF Converter</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 40px 20px;
            color: #333;
        }
        
        .container {
            width: 100%;
            max-width: 800px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }
        
        header {
            background: #764ba2;
            color: white;
            padding: 25px;
            text-align: center;
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .upload-container {
            padding: 30px;
            text-align: center;
        }
        
        .upload-area {
            border: 3px dashed #764ba2;
            border-radius: 12px;
            padding: 40px 20px;
            margin: 20px 0;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .upload-area:hover {
            background: #f8f6ff;
        }
        
        .upload-area i {
            font-size: 60px;
            color: #764ba2;
            margin-bottom: 15px;
        }
        
        .upload-text {
            font-size: 1.2rem;
            margin-bottom: 10px;
        }
        
        .file-input {
            display: none;
        }
        
        .browse-btn {
            background: #764ba2;
            color: white;
            padding: 12px 30px;
            border-radius: 50px;
            cursor: pointer;
            display: inline-block;
            margin-top: 15px;
            font-weight: 600;
            transition: all 0.3s;
        }
        
        .browse-btn:hover {
            background: #667eea;
            transform: translateY(-2px);
        }
        
        .file-info {
            text-align: left;
            background: #f5f3ff;
            padding: 15px;
            border-radius: 8px;
            margin: 20px 0;
            display: none;
        }
        
        .file-info h3 {
            margin-bottom: 10px;
            color: #764ba2;
        }
        
        .action-buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 25px;
        }
        
        .btn {
            padding: 12px 25px;
            border-radius: 50px;
            border: none;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            justify-content: center;
        }
        
        .btn i {
            margin-right: 8px;
        }
        
        .convert-btn {
            background: #764ba2;
            color: white;
        }
        
        .convert-btn:hover {
            background: #667eea;
        }
        
        .download-btn {
            background: #28a745;
            color: white;
            display: none;
        }
        
        .download-btn:hover {
            background: #218838;
        }
        
        .supported-files {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 8px;
            margin-top: 30px;
        }
        
        .supported-files h3 {
            color: #764ba2;
            margin-bottom: 15px;
            text-align: center;
        }
        
        .file-types {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 15px;
        }
        
        .file-type {
            background: white;
            padding: 10px 20px;
            border-radius: 50px;
            box-shadow: 0 3px 8px rgba(0,0,0,0.1);
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .file-type i {
            color: #764ba2;
        }
        
        footer {
            text-align: center;
            margin-top: 30px;
            color: white;
            opacity: 0.8;
        }
        
        @media (max-width: 600px) {
            h1 {
                font-size: 1.8rem;
            }
            
            .action-buttons {
                flex-direction: column;
            }
            
            .btn {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>File to PDF Converter</h1>
            <p class="subtitle">Convert any document to PDF format</p>
        </header>
        
        <div class="upload-container">
            <div class="upload-area" id="uploadArea">
                <i class="fas fa-file-upload"></i>
                <p class="upload-text">Drag & drop your file here</p>
                <p>or</p>
                <div class="browse-btn">Browse Files</div>
                <input type="file" id="fileInput" class="file-input">
            </div>
            
            <div class="file-info" id="fileInfo">
                <h3>Selected File:</h3>
                <p id="fileName"></p>
                <p id="fileSize"></p>
            </div>
            
            <div class="action-buttons">
                <button class="btn convert-btn" id="convertBtn">
                    <i class="fas fa-sync-alt"></i> Convert to PDF
                </button>
                <a class="btn download-btn" id="downloadBtn" download>
                    <i class="fas fa-download"></i> Download PDF
                </a>
            </div>
        </div>
        
        <div class="supported-files">
            <h3>Supported File Types</h3>
            <div class="file-types">
                <div class="file-type"><i class="fas fa-file-word"></i> DOC/DOCX</div>
                <div class="file-type"><i class="fas fa-file-excel"></i> XLS/XLSX</div>
                <div class="file-type"><i class="fas fa-file-powerpoint"></i> PPT/PPTX</div>
                <div class="file-type"><i class="fas fa-file-image"></i> JPG/PNG</div>
                <div class="file-type"><i class="fas fa-file-alt"></i> TXT</div>
            </div>
        </div>
    </div>
    
    <footer>
        <p>© 2023 File to PDF Converter | For demonstration purposes</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const uploadArea = document.getElementById('uploadArea');
            const fileInput = document.getElementById('fileInput');
            const fileInfo = document.getElementById('fileInfo');
            const fileName = document.getElementById('fileName');
            const fileSize = document.getElementById('fileSize');
            const convertBtn = document.getElementById('convertBtn');
            const downloadBtn = document.getElementById('downloadBtn');
            
            let selectedFile = null;
            
            // Click on upload area to trigger file input
            uploadArea.addEventListener('click', function() {
                fileInput.click();
            });
            
            // Drag and drop functionality
            uploadArea.addEventListener('dragover', function(e) {
                e.preventDefault();
                uploadArea.style.borderColor = '#667eea';
                uploadArea.style.backgroundColor = '#f0edff';
            });
            
            uploadArea.addEventListener('dragleave', function() {
                uploadArea.style.borderColor = '#764ba2';
                uploadArea.style.backgroundColor = 'transparent';
            });
            
            uploadArea.addEventListener('drop', function(e) {
                e.preventDefault();
                uploadArea.style.borderColor = '#764ba2';
                uploadArea.style.backgroundColor = 'transparent';
                
                if (e.dataTransfer.files.length) {
                    handleFile(e.dataTransfer.files[0]);
                }
            });
            
            // File input change event
            fileInput.addEventListener('change', function() {
                if (fileInput.files.length) {
                    handleFile(fileInput.files[0]);
                }
            });
            
            // Handle the selected file
            function handleFile(file) {
                selectedFile = file;
                
                // Display file information
                fileName.textContent = `Name: ${file.name}`;
                fileSize.textContent = `Size: ${formatFileSize(file.size)}`;
                fileInfo.style.display = 'block';
                
                // Show convert button
                convertBtn.style.display = 'inline-flex';
                downloadBtn.style.display = 'none';
            }
            
            // Format file size
            function formatFileSize(bytes) {
                if (bytes === 0) return '0 Bytes';
                const k = 1024;
                const sizes = ['Bytes', 'KB', 'MB', 'GB'];
                const i = Math.floor(Math.log(bytes) / Math.log(k));
                return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
            }
            
            // Convert button event
            convertBtn.addEventListener('click', function() {
                if (!selectedFile) return;
                
                // Simulate conversion process
                convertBtn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Converting...';
                convertBtn.disabled = true;
                
                // In a real application, this would be an actual conversion process
                setTimeout(function() {
                    // Simulate successful conversion
                    convertBtn.innerHTML = '<i class="fas fa-check"></i> Conversion Complete!';
                    convertBtn.style.background = '#28a745';
                    
                    // Enable download button
                    downloadBtn.style.display = 'inline-flex';
                    
                    // Set up download
                    const pdfFileName = selectedFile.name.split('.')[0] + '.pdf';
                    downloadBtn.setAttribute('download', pdfFileName);
                    
                    // In a real application, this would be the actual PDF data
                    // For demo purposes, we're using a dummy URL
                    downloadBtn.setAttribute('href', '#');
                    
                    // Reset convert button after a while
                    setTimeout(function() {
                        convertBtn.innerHTML = '<i class="fas fa-sync-alt"></i> Convert to PDF';
                        convertBtn.style.background = '#764ba2';
                        convertBtn.disabled = false;
                    }, 2000);
                }, 2000);
            });
            
            // Download button event
            downloadBtn.addEventListener('click', function() {
                // In a real application, this would download the actual converted PDF
                alert('In a real application, this would download the converted PDF file. This is a frontend demonstration.');
            });
        });
    </script>
</body>
</html>
