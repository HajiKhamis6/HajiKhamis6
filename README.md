<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>O.C app</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/intl-tel-input@17.0.12/build/css/intlTelInput.css">
    <style>
        /* Main App Styles */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            width:100%;
           max-width: 600px;
background-colorkground-col    #f4f4f4;display: flex;
            flex-direction: column;
            align-items: center;
        }

        header {
            color: white;
            text-align: center;
            padding: 15px;
            width: 90%;
            font-size: 35px;
            position: fixed;
            top: 0;
            z-index: 100;
            background-color: #f4f4f4;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        header span.oc {
            background: linear-gradient(to right, red, blue, gold, darkred);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-weight: bold;
        }

        header span.app {
            background: linear-gradient(to right, green, red, gold);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-weight: bold;
        }

        /* Content Container */
        .content-container {
            margin-top: 100px;
            width: 100%;
            max-width: 600px;
            padding: 0 15px;
            box-sizing: border-box;
            margin-bottom: 80px;
        }

        /* Market Button */
        .market-button, .qr-button {
            position: fixed;
            top: 15px;
            width: 45px;
            height: 45px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 20px;
            cursor: pointer;
            background-color: #fff;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
            border: none;
            z-index: 100;
        }

        .market-button {
            right: 15px;
        }

        .qr-button {
            left: 15px;
        }

        .market-button:hover, .qr-button:hover {
            background-color: #f0f0f0;
            transform: scale(1.05);
            transition: all 0.2s ease;
        }

        /* Post Styles */
        .post {
            position: relative;
            width: 100%;
            background: #000;
            border-radius: 10px;
            overflow: hidden;
            margin-bottom: 30px;
        }
        
        .post-header {
            display: flex;
            align-items: center;
            padding: 10px;
            background: #fff;
        }
        
        .post-profile-pic {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            margin-right: 10px;
        }
        
        .post-username {
            font-weight: bold;
        }
        
        .post-media {
            width: 100%;
            display: block;
        }
        
        .post-video {
            width: 100%;
            height: 400px;
            aspect-ratio: 9/5;
            object-fit: fill;
            background: #000;
        }
        
        .post-image {
            width: 100%;
            max-height: 600px;
            object-fit: contain;
            background-color: #000;
        }
        
        .post-actions {
            display: flex;
            flex-direction: column;
            position: absolute;
            right: 10px;
            bottom: 15px;
            z-index: 10;
            padding: 5px;
        }
        
        .post-action-button {
            width: 45px;
            height: 45px;
            margin: 5px 0;
            border-radius: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 15px;
            cursor: pointer;
            background-color: rgba(255,255,255,0.7);
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
            border: none;
        }
        
        .post-stats {
            padding: 10px;
            background: #fff;
            color: #333;
        }
        
        .post-comments {
            position: absolute;
            bottom: 0;
            display: none;
            background: #fff;
            padding: 10px;
            height: 150px;
            overflow-y: auto;
            z-index: 5;
            width: 100%;
            box-sizing: border-box;
        }

        /* Comment Styles */
        .comment {
            padding: 8px;
            margin: 5px 0;
            background: #f5f5f5;
            border-radius: 5px;
            position: relative;
        }

        .comment-actions {
            position: absolute;
            right: 5px;
            top: 5px;
            display: none;
        }

        .comment:hover .comment-actions {
            display: block;
        }

        .comment-action {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 12px;
            margin-left: 5px;
            color: #666;
        }

        .replying-to {
            font-size: 12px;
            color: #555;
            background: #f0f0f0;
            padding: 5px;
            border-radius: 5px;
            margin-bottom: 5px;
        }

        .delete-confirm {
            background-color: #ffebee;
            padding: 5px;
            margin-top: 5px;
            border-radius: 5px;
            display: none;
        }

        /* Footer Styles */
        .footer {
            position: fixed;
            bottom: 0;
            display: flex;
            justify-content: center;
            gap: 60px;
            width: 100%;
            background: #f4f4f4;
            padding: 10px 0;
            box-shadow: 0 -2px 5px rgba(0,0,0,0.1);
        }

        .footer-button {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px;
            cursor: pointer;
            background-color: #fff;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
        }

        .footer-button.upload {
            background-color: #32cd32;
            color: white;
        }

        /* Market Section Styles */
        #market-section, #qr-section {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 0 15px rgba(0,0,0,0.1);
            width: 90%;
            max-width: 500px;
            max-height: 80vh;
            overflow-y: auto;
            z-index: 1000;
        }

        /* Profile Settings */
        .profile-settings {
            display: none;
            flex-direction: column;
            gap: 15px;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            padding: 20px;
            background: purple;
            border-radius: 15px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
            width: 90%;
            max-width: 400px;
            max-height: 80vh;
            overflow-y: auto;
            z-index: 1000;
        }

        .profile-settings input {
            width: 100%;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 50px;
            box-sizing: border-box;
        }

        .profile-settings img {
            max-width: 80px;
            border-radius: 50%;
            margin: 10px auto;
            display: block;
        }

        .close-button, .save-button {
            background: red;
            color: white;
            font-weight: bold;
            border: none;
            padding: 12px;
            cursor: pointer;
            border-radius: 50px;
            width: 100%;
            margin-top: 10px;
        }
        
        .close-button {
            background: #ff4d4d;
        }
        
        .search-container {
            background-color: blue; 
            color: white;
            font-weight: bold;
            border: none;
            padding: 12px;
            cursor: pointer;
            border-radius: 50px;
            width: 100%;
            text-align: center;
        }

        /* Account Creation Styles */
        .account-section {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
            border-left: 4px solid #3498db;
        }

        .account-section h3 {
            margin-top: 0;
            color: #2c3e50;
            border-bottom: 1px solid #ddd;
            padding-bottom: 8px;
        }

        .password-field {
            position: relative;
            display: flex;
            align-items: center;
        }

        .password-field input {
            flex: 1;
            padding-right: 35px;
        }

        .toggle-password {
            position: absolute;
            right: 10px;
            cursor: pointer;
            user-select: none;
        }

        .password-strength {
            margin-top: 8px;
            display: flex;
            align-items: center;
        }

        .strength-bar {
            height: 5px;
            flex-grow: 1;
            background: #e0e0e0;
            border-radius: 3px;
            margin-right: 10px;
            overflow: hidden;
        }

        .strength-bar::after {
            content: '';
            display: block;
            height: 100%;
            width: 0%;
            background: red;
            transition: width 0.3s, background 0.3s;
        }

        .strength-text {
            font-size: 12px;
            color: #666;
        }

        .password-requirements {
            margin-top: 15px;
            font-size: 13px;
            color: #555;
        }

        .password-requirements ul {
            margin: 5px 0 0 20px;
            padding: 0;
        }

        .password-requirements li {
            margin-bottom: 3px;
            color: #e74c3c;
        }

        .password-requirements li.valid {
            color: #2ecc71;
        }

        /* Global Chat Platform Styles */
        #chat-section {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            border: 1px solid #ccc;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
            width: 340px;
            text-align: center;
            z-index: 1000;
        }

        .chat-header {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }

        .chat-header img {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            margin-right: 10px;
        }

        #chat-box {
            border: 1px solid #ddd;
            height: 350px;
            overflow-y: auto;
            margin-bottom: 10px;
            padding: 5px;
            background: #fff;
            display: flex;
            flex-direction: column;
        }

        .message {
            padding: 10px;
            margin: 5px;
            border-radius: 8px;
            max-width: 60%;
            cursor: pointer;
            position: relative;
        }

        .message.sent {
            background: #d1e7ff;
            align-self: flex-end;
        }

        .message.received {
            background: #e2e2e2;
            align-self: flex-start;
        }

        /* Market Form Styles */
        #market-section h2 {
            text-align: center;
            color: #333;
        }

        #market-section::-webkit-scrollbar, 
        #qr-section::-webkit-scrollbar,
        .profile-settings::-webkit-scrollbar {
            width: 8px;
        }

        #market-section::-webkit-scrollbar-thumb, 
        #qr-section::-webkit-scrollbar-thumb,
        .profile-settings::-webkit-scrollbar-thumb {
            background: #888;
            border-radius: 4px;
        }

        #productForm {
            max-height: calc(80vh - 100px);
            overflow-y: auto;
        }

        #market-section input, 
        #market-section textarea, 
        #market-section select {
            width: 100%;
            margin: 10px 0;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 10px;
            font-size: 18px;
            box-sizing: border-box;
        }

        #market-section input[type="file"] {
            border: none;
        }

        #market-section button[type="submit"] {
            width: 100%;
            padding: 12px;
            font-size: 16px;
            font-weight: bold;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            margin-top: 10px;
            background-color: #28a745;
            color: white;
            transition: background-color 0.3s;
        }

        #market-section button[type="submit"]:hover {
            background-color: #218838;
        }

        .image-preview {
            display: flex;
            overflow-x: auto;
            gap: 10px;
            margin-top: 10px;
            padding-bottom: 10px;
            scroll-behavior: smooth;
        }

        .image-preview img {
            height: 150px;
            border-radius: 10px;
            object-fit: cover;
        }

        .success, .error {
            text-align: center;
            margin-top: 15px;
            font-weight: bold;
        }

        .success {
            color: green;
        }

        .error {
            color: red;
        }

        .loader {
            display: none;
            text-align: center;
            margin-top: 10px;
            color: #333;
        }

        /* Choose Friend Section */
        #choose-friend-section {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            border: 1px solid #ccc;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            width: 90%;
            max-height:50%;
            text-align: center;
            z-index: 1000;
        }

        #choose-friend-section h3 {
            margin-bottom: 10px;
        }

        #friend-list {
            max-height: 200px;
            overflow-y: auto;
            margin-bottom: 10px;
        }

        .friend-item {
            display: flex;
            align-items: center;
            padding: 10px;
            border-bottom: 1px solid #ddd;
            cursor: pointer;
        }

        .friend-item img {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            margin-right: 10px;
        }

        .friend-item:hover {
            background-color: #f0f0f0;
        }
        
        /* QR Code Controller Styles */
        .qr-controller-container {
            background-color: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            margin-bottom: 30px;
            width: 96%;
        }
        
        .qr-controller-container h1 {
            color: #2c3e50;
            text-align: center;
            margin-bottom: 30px;
        }
        
        .qr-display {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin: 20px 0;
        }
        
        #qrcodeCanvas {
            width: 200px;
            height: 200px;
            border: 1px solid #ddd;
            margin: 15px 0;
        }
        
        .qr-controls {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
            margin: 20px 0;
        }
        
        .qr-control-group {
            display: flex;
            flex-direction: column;
            min-width: 200px;
        }
        
        .qr-control-group label {
            margin-bottom: 5px;
            font-weight: bold;
            color: #34495e;
        }
        
        .qr-control-group input, 
        .qr-control-group select, 
        .qr-control-group button {
            padding: 8px 12px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 14px;
        }
        
        .qr-control-group button {
            background-color: #3498db;
            color: white;
            border: none;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        .qr-control-group button:hover {
            background-color: #2980b9;
        }
        
        .qr-details-panel {
            background-color: #f8f9fa;
            padding: 15px;
            border-radius: 5px;
            margin-top: 20px;
            border-left: 4px solid #3498db;
        }
        
        .qr-details-title {
            font-weight: bold;
            margin-bottom: 10px;
            color: #2c3e50;
        }
        
        .qr-detail-item {
            margin-bottom: 0px;
            display: flex;
        }
        
        .qr-detail-label {
            font-weight: bold;
            min-width: 120px;
            color: #7f8c8d;
        }
        
        .qr-detail-value {
            word-break: break-all;
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <span class="oc">☆O.C</span> <span class="app">app☆ 22/05/2025</span>
    </header>

    <!-- QR Code Button -->
    <button class="qr-button" onclick="openQRController()">🔲</button>
    
    <!-- Market Button -->
    <button class="market-button" onclick="openMarket()">🚞</button>

    <!-- Content Container -->
    <div class="content-container">
        <!-- Posts Container -->
        <div id="posts-container">
            <!-- Posts will be added here dynamically -->
        </div>
    </div>

    <!-- Footer -->
    <div class="footer">
        <div class="footer-button profile" onclick="openProfile()">👤</div>
        
        <!-- Image Upload Button -->
        <div class="footer-button upload">
            <label for="image-upload-input" style="cursor: pointer;">🖼️</label>
            <input id="image-upload-input" type="file" accept="image/*" style="display: none;" onchange="uploadImage()">
        </div>
        
        <!-- Video Upload Button -->
        <div class="footer-button upload">
            <label for="video-upload-input" style="cursor: pointer;">📤</label>
            <input id="video-upload-input" type="file" accept="video/*" style="display: none;" onchange="uploadVideo()">
        </div>
        
        <div class="footer-button home" onclick="goHome()">🏡</div>
    </div>
    
    <!-- QR Code Section -->
    <div id="qr-section">
        <button class="close-button" onclick="closeQRController()">Close</button>
        <div class="qr-controller-container">
            <h1>QR Code Controller</h1>
            
            <div class="qr-display">
                <canvas id="qrcodeCanvas"></canvas>
                <div id="downloadSection" style="display: none;">
                    <button id="downloadBtn">Download QR Code</button>
                </div>
            </div>
            
            <div class="qr-controls">
                <div class="qr-control-group">
                    <label for="qrContent">QR Content:</label>
                    <input type="text" id="qrContent" value="https://example.com" placeholder="Enter URL or text">
                </div>
                
                <div class="qr-control-group">
                    <label for="qrSize">Size:</label>
                    <select id="qrSize">
                        <option value="100">100x100</option>
                        <option value="150">150x150</option>
                        <option value="200" selected>200x200</option>
                        <option value="250">250x250</option>
                        <option value="300">300x300</option>
                    </select>
                </div>
                
                <div class="qr-control-group">
                    <label for="qrColor">Color:</label>
                    <input type="color" id="qrColor" value="#000000">
                </div>
                
                <div class="qr-control-group">
                    <label for="qrBgColor">Background:</label>
                    <input type="color" id="qrBgColor" value="#ffffff">
                </div>
            </div>
            
            <div class="qr-controls">
                <button id="generateBtn">Generate QR Code</button>
                <button id="resetBtn">Reset Settings</button>
            </div>
            
            <div class="qr-details-panel">
                <div class="qr-details-title">QR Code Information</div>
                <div class="qr-detail-item">
                    <div class="qr-detail-label">Content Type:</div>
                    <div class="qr-detail-value" id="infoType">URL</div>
                </div>
                <div class="qr-detail-item">
                    <div class="qr-detail-label">Content Length:</div>
                    <div class="qr-detail-value" id="infoLength">19 characters</div>
                </div>
                <div class="qr-detail-item">
                    <div class="qr-detail-label">Generation Date:</div>
                    <div class="qr-detail-value" id="infoDate"></div>
                </div>
                <div class="qr-detail-item">
                    <div class="qr-detail-label">QR Code Size:</div>
                    <div class="qr-detail-value" id="infoSize">200x200 px</div>
                </div>
                <div class="qr-detail-item">
                    <div class="qr-detail-label">Color Scheme:</div>
                    <div class="qr-detail-value" id="infoColors">Black on White</div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Market Section -->
    <div id="market-section">
        <button class="close-button" onclick="closeMarket()">Close</button>
        <h2>KEEP YOUR BUSINESS ON MARKET</h2>
        <form id="productForm">
            <input type="text" id="companyName" placeholder="Jina la Kampuni" required />
            <input type="text" id="productName" placeholder="Jina la Bidhaa" required />
            <input type="number" id="productPrice" placeholder="Bei (TZS)" required />
            <input type="number" id="transactionsNumber" placeholder="Namba ya muamala benki/simu" required/>
            <textarea id="productDesc" placeholder="Maelezo ya Bidhaa" required></textarea>
            <input type="text" id="contact" placeholder="Simu/Barua Pepe" required/>
            <select id="paymentMethod" required>
                <option value="">Chagua Njia ya Malipo</option>
                <option value="bank">Benki</option>
                <option value="mobile">Malipo kwa Simu</option>
            </select>

            <input type="file" id="productImages" accept="image/*" multiple required />
            <div class="image-preview" id="imagePreview"></div>

            <button type="submit">Wasilisha Bidhaa</button>
            <div class="loader" id="loader">Inatuma bidhaa...</div>
            <div class="success" id="successMessage"></div>
            <div class="error" id="errorMessage"></div>
        </form>
    </div>

    <!-- Profile Settings -->
    <div class="profile-settings" id="profile-settings">
        <button class="close-button" onclick="closeProfile()">Close</button>
        <input type="hidden" id="storage-url" value="https://appurl.io/BxMDQ060Qj">
        
        <!-- Account Creation Section -->
        <div class="account-section">
            <h3>Account Information</h3>
            <input type="email" id="profile-email" placeholder="Email Address" required>
            <div class="password-field">
                <input type="password" id="profile-password" placeholder="Password (min 8 characters)" required>
                <span class="toggle-password" onclick="togglePasswordVisibility()">👁️</span>
            </div>
            <div class="password-strength" id="password-strength">
                <div class="strength-bar"></div>
                <span class="strength-text">Weak</span>
            </div>
            <div class="password-requirements">
                <p>Password must contain:</p>
                <ul>
                    <li id="req-length">At least 8 characters</li>
                    <li id="req-upper">Uppercase letter</li>
                    <li id="req-lower">Lowercase letter</li>
                    <li id="req-number">Number</li>
                    <li id="req-special">Special character</li>
                </ul>
            </div>
        </div>
        
        <button class="search-container" onclick="searchInput()">MESSAGE</button>
        <input type="text" id="profile-name" placeholder="Name">
        <input type="date" id="profile-dob" placeholder="Date of Birth">
        <input type="file" accept="image/*" onchange="previewImage(event)">
        <img id="profile-pic" src="" alt="Profile Picture">
        <button class="save-button" onclick="saveProfile()">Save</button>
    </div>

    <!-- Global Chat Platform -->
    <div id="chat-section">
        <button id="back-button" onclick="goBack()">Back</button>
        <div class="chat-header">
            <input type="file" accept="image/*" onchange="previewImage(event)">
            <img id="profile-pic" src="" alt="Profile picture">
            <input type="text" id="profile-name" placeholder="Name">
        </div>
        <div id="chat-box"></div>
        <div id="replying-to" class="replying-to" style="display: none;"></div>
        <input type="text" id="message-input" placeholder="Type a message...">
        <button onclick="sendMessage()">Send</button>
    </div>
    
    <!-- Choose Friend Section -->
    <div id="choose-friend-section">
        <h3>Choose a Friend</h3>
        <div id="friend-list">
            <div class="friend-item" onclick="selectFriend('Friend 1', 'friend1.jpg')">
                <img src="friend1.jpg" alt="Friend 1">
                <span>Friend 1</span>
            </div>
            <div class="friend-item" onclick="selectFriend('Friend 2', 'friend2.jpg')">
                <img src="friend2.jpg" alt="Friend 2">
                <span>Friend 2</span>
            </div>
            <div class="friend-item" onclick="selectFriend('Friend 3', 'friend3.jpg')">
                <img src="friend3.jpg" alt="Friend 3">
                <span>Friend 3</span>
            </div>
        </div>
        <button onclick="closeChooseFriend()">Close</button>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/intl-tel-input@17.0.12/build/js/intlTelInput.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.1/build/qrcode.min.js"></script>
    <script>
        // Store user information
        const currentUser = {
            name: "Current User",
            email: "",
            profilePic: "https://via.placeholder.com/150"
        };
        
        // Array to store all posts
        let posts = [];
        
        // Function to create a new post
        function createPost(mediaFile, user, isImage = false) {
            const postsContainer = document.getElementById('posts-container');
            const postId = 'post-' + Date.now();
            
            const postElement = document.createElement('div');
            postElement.className = 'post';
            postElement.id = postId;
            
            postElement.innerHTML = `
                <div class="post-header">
                    <img src="${user.profilePic}" class="post-profile-pic">
                    <span class="post-username">${user.name}</span>
                </div>
                ${isImage ? 
                    '<img class="post-image" src="" alt="Posted image">' : 
                    '<video class="post-video" controls>Your browser does not support the video tag.</video>'
                }
                <div class="post-actions">
                    <button class="post-action-button like-button" onclick="toggleLike('${postId}')">💖</button>
                    <span class="like-count" id="${postId}-like-count">0</span>
                    <button class="post-action-button comment-button" onclick="toggleComment('${postId}')">💬</button>
                    <button class="post-action-button share-button" onclick="sharePost('${postId}')">📤</button>
                </div>
                <div class="post-stats">
                    <div>Likes: <span id="${postId}-like-count-display">0</span></div>
                </div>
                <div class="post-comments" id="${postId}-comments">
                    <textarea placeholder="Write a comment..." style="width:100%; height:60px;"></textarea>
                    <button onclick="postComment('${postId}')">Post</button>
                    <div class="comments-list"></div>
                </div>
            `;
            
            postsContainer.insertBefore(postElement, postsContainer.firstChild);
            
            const mediaElement = postElement.querySelector(isImage ? '.post-image' : '.post-video');
            mediaElement.src = URL.createObjectURL(mediaFile);
            
            posts.push({
                id: postId,
                user: user,
                media: mediaFile,
                isImage: isImage,
                likes: 0,
                liked: false,
                comments: []
            });
        }
        
        // Function to handle image upload
        function uploadImage() {
            const fileInput = document.getElementById('image-upload-input');
            const file = fileInput.files[0];
            
            if (file) {
                createPost(file, currentUser, true);
                fileInput.value = '';
            } else {
                alert("Please select an image to upload.");
            }
        }
        
        // Function to handle video upload
        function uploadVideo() {
            const fileInput = document.getElementById('video-upload-input');
            const file = fileInput.files[0];
            
            if (file) {
                createPost(file, currentUser, false);
                fileInput.value = '';
            } else {
                alert("Please select a video to upload.");
            }
        }
        
        // Post-specific functions
        function toggleLike(postId) {
            const post = posts.find(p => p.id === postId);
            if (post) {
                post.liked = !post.liked;
                post.likes += post.liked ? 1 : -1;
                
                document.getElementById(`${postId}-like-count`).innerText = post.likes;
                document.getElementById(`${postId}-like-count-display`).innerText = post.likes;
                
                const button = document.querySelector(`#${postId} .like-button`);
                button.classList.toggle('active');
            }
        }
        
        function toggleComment(postId) {
            const commentsSection = document.getElementById(`${postId}-comments`);
            commentsSection.style.display = commentsSection.style.display === 'none' ? 'block' : 'none';
        }
        
        // Track which comment is being replied to for each post
        let replyingToComments = {};

        function postComment(postId) {
            const commentInput = document.querySelector(`#${postId}-comments textarea`);
            const commentText = commentInput.value.trim();
            const commentsList = document.querySelector(`#${postId}-comments .comments-list`);
            
            if (commentText) {
                const post = posts.find(p => p.id === postId);
                const isReplying = replyingToComments[postId];
                
                const commentData = {
                    id: 'comment-' + Date.now(),
                    user: currentUser,
                    text: commentText,
                    timestamp: new Date(),
                    replyTo: isReplying ? isReplying.commentId : null
                };
                
                post.comments.push(commentData);
                
                const commentElement = document.createElement('div');
                commentElement.className = 'comment';
                commentElement.id = commentData.id;
                
                let replyText = '';
                if (commentData.replyTo) {
                    const repliedComment = post.comments.find(c => c.id === commentData.replyTo);
                    if (repliedComment) {
                        replyText = `<div class="replying-to">Replying to ${repliedComment.user.name}: ${repliedComment.text.substring(0, 30)}...</div>`;
                    }
                }
                
                commentElement.innerHTML = `
                    ${replyText}
                    <img src="${currentUser.profilePic}" width="30" height="30" style="border-radius:50%;">
                    <strong>${currentUser.name}:</strong> ${commentText}
                    <div class="comment-actions">
                        <button class="comment-action" onclick="setReply('${postId}', '${commentData.id}')">↩️</button>
                        <button class="comment-action" onclick="showDeleteConfirm('${postId}', '${commentData.id}')">🗑️</button>
                    </div>
                    <div class="delete-confirm" id="delete-confirm-${commentData.id}">
                        Delete this comment?
                        <button onclick="deleteComment('${postId}', '${commentData.id}')">Yes</button>
                        <button onclick="hideDeleteConfirm('${commentData.id}')">No</button>
                    </div>
                `;
                
                commentsList.appendChild(commentElement);
                
                if (isReplying) {
                    document.getElementById(`replying-to-${postId}`).style.display = 'none';
                    replyingToComments[postId] = null;
                }
                
                commentInput.value = '';
            }
        }

        function setReply(postId, commentId) {
            const post = posts.find(p => p.id === postId);
            const comment = post.comments.find(c => c.id === commentId);
            
            replyingToComments[postId] = {
                commentId: commentId,
                userName: comment.user.name,
                commentText: comment.text
            };
            
            const replyIndicator = document.getElementById(`replying-to-${postId}`);
            replyIndicator.innerHTML = `Replying to ${comment.user.name}: ${comment.text.substring(0, 50)}... <button onclick="cancelReply('${postId}')">✖</button>`;
            replyIndicator.style.display = 'block';
            
            document.querySelector(`#${postId}-comments textarea`).focus();
        }

        function cancelReply(postId) {
            replyingToComments[postId] = null;
            document.getElementById(`replying-to-${postId}`).style.display = 'none';
        }

        function showDeleteConfirm(postId, commentId) {
            document.getElementById(`delete-confirm-${commentId}`).style.display = 'block';
        }

        function hideDeleteConfirm(commentId) {
            document.getElementById(`delete-confirm-${commentId}`).style.display = 'none';
        }

        function deleteComment(postId, commentId) {
            const post = posts.find(p => p.id === postId);
            post.comments = post.comments.filter(c => c.id !== commentId);
            
            const commentElement = document.getElementById(commentId);
            if (commentElement) {
                commentElement.remove();
            }
        }

        function sharePost(postId) {
            alert(`Sharing post ${postId}`);
        }
        
        // Profile image preview
        function previewImage(event) {
            const img = document.getElementById('profile-pic');
            if (img) {
                img.src = URL.createObjectURL(event.target.files[0]);
                img.onload = () => URL.revokeObjectURL(img.src);
                currentUser.profilePic = img.src;
            }
        }
        
        // Market functions
        function openMarket() {
            document.getElementById('market-section').style.display = 'block';
        }
        
        function closeMarket() {
            document.getElementById('market-section').style.display = 'none';
        }
        
        // QR Controller functions
        function openQRController() {
            document.getElementById('qr-section').style.display = 'block';
        }
        
        function closeQRController() {
            document.getElementById('qr-section').style.display = 'none';
        }
        
        // Profile functions
        function openProfile() {
            document.getElementById('profile-settings').style.display = 'flex';
        }
        
        function closeProfile() {
            document.getElementById('profile-settings').style.display = 'none';
        }
        
        function searchInput() {
            document.getElementById('profile-settings').style.display = 'none';
            document.getElementById('chat-section').style.display = 'block';
        }

        // Password validation functions
        function checkPasswordStrength(password) {
            let strength = 0;
            const requirements = {
                length: password.length >= 8,
                upper: /[A-Z]/.test(password),
                lower: /[a-z]/.test(password),
                number: /[0-9]/.test(password),
                special: /[^A-Za-z0-9]/.test(password)
            };

            Object.keys(requirements).forEach(req => {
                const element = document.getElementById(`req-${req}`);
                if (requirements[req]) {
                    element.classList.add('valid');
                    strength++;
                } else {
                    element.classList.remove('valid');
                }
            });

            const strengthBar = document.querySelector('.strength-bar');
            const strengthText = document.querySelector('.strength-text');
            
            let width = 0;
            let color = '';
            let text = '';
            
            if (strength <= 1) {
                width = 25;
                color = '#e74c3c';
                text = 'Weak';
            } else if (strength <= 3) {
                width = 50;
                color = '#f39c12';
                text = 'Medium';
            } else if (strength <= 4) {
                width = 75;
                color = '#3498db';
                text = 'Strong';
            } else {
                width = 100;
                color = '#2ecc71';
                text = 'Very Strong';
            }
            
            strengthBar.style.width = `${width}%`;
            strengthBar.style.backgroundColor = color;
            strengthText.textContent = text;
            strengthText.style.color = color;
            
            return strength >= 3;
        }

        function togglePasswordVisibility() {
            const passwordField = document.getElementById('profile-password');
            passwordField.type = passwordField.type === 'password' ? 'text' : 'password';
        }

        document.getElementById('profile-password').addEventListener('input', function() {
            checkPasswordStrength(this.value);
        });

        function saveProfile() {
            const name = document.getElementById('profile-name').value;
            const email = document.getElementById('profile-email').value;
            const password = document.getElementById('profile-password').value;
            const dob = document.getElementById('profile-dob').value;
            const storageUrl = document.getElementById('storage-url').value;

            if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) {
                alert('Please enter a valid email address!');
                return;
            }

            if (!checkPasswordStrength(password)) {
                alert('Please choose a stronger password!');
                return;
            }

            if (!name || !dob) {
                alert('Please fill in all fields!');
                return;
            }

            currentUser.name = name;
            currentUser.email = email;

            fetch(storageUrl, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ 
                    name, 
                    email, 
                    password, 
                    dob 
                }),
            })
            .then(response => response.json())
            .then(data => {
                alert(`Profile Saved! Response: ${JSON.stringify(data)}`);
                closeProfile();
            })
            .catch(error => alert(`Error saving profile: ${error.message}`));
        }

        function goHome() {
            alert('Returning to Home Page!');
        }       
        
        // Market Section Script
        const productImages = document.getElementById('productImages');
        const imagePreview = document.getElementById('imagePreview');
        const successMessage = document.getElementById('successMessage');
        const errorMessage = document.getElementById('errorMessage');
        const loader = document.getElementById('loader');

        productImages.addEventListener('change', function() {
            imagePreview.innerHTML = '';
            const files = this.files;

            if (files.length > 0) {
                Array.from(files).forEach(file => {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        const img = document.createElement('img');
                        img.src = e.target.result;
                        imagePreview.appendChild(img);
                    };
                    reader.readAsDataURL(file);
                });
            }
        });

        document.getElementById('productForm').addEventListener('submit', async function(e) {
            e.preventDefault();

            successMessage.innerText = '';
            errorMessage.innerText = '';
            loader.style.display = 'block';

            const formData = new FormData();
            formData.append('companyName', document.getElementById('companyName').value);
            formData.append('productName', document.getElementById('productName').value);
            formData.append('productPrice', document.getElementById('productPrice').value);
            formData.append('productDesc', document.getElementById('productDesc').value);
            formData.append('paymentMethod', document.getElementById('paymentMethod').value);

            Array.from(productImages.files).forEach(file => {
                formData.append('productImages', file);
            });

            try {
                const res = await fetch('http://localhost:3000/api/products', {
                    method: 'POST',
                    body: formData
                });

                const result = await res.json();
                if (res.ok) {
                    successMessage.innerText = result.message || "Your product has been submitted successfully!";
                    this.reset();
                    imagePreview.innerHTML = '';
                } else {
                    errorMessage.innerText = result.message || "An error occurred.";
                }
            } catch (error) {
                console.error(error);
                errorMessage.innerText = "Network or server error. Please try again.";
            } finally {
                loader.style.display = 'none';
            }
        });

        // QR Code Controller Script
        document.addEventListener('DOMContentLoaded', function() {
            const qrContent = document.getElementById('qrContent');
            const qrSize = document.getElementById('qrSize');
            const qrColor = document.getElementById('qrColor');
            const qrBgColor = document.getElementById('qrBgColor');
            const generateBtn = document.getElementById('generateBtn');
            const resetBtn = document.getElementById('resetBtn');
            const downloadBtn = document.getElementById('downloadBtn');
            const canvas = document.getElementById('qrcodeCanvas');
            const downloadSection = document.getElementById('downloadSection');
            
            const infoType = document.getElementById('infoType');
            const infoLength = document.getElementById('infoLength');
            const infoDate = document.getElementById('infoDate');
            const infoSize = document.getElementById('infoSize');
            const infoColors = document.getElementById('infoColors');
            
            function generateQRCode() {
                const content = qrContent.value;
                const size = parseInt(qrSize.value);
                const color = qrColor.value;
                const bgColor = qrBgColor.value;
                
                infoType.textContent = content.startsWith('http') ? 'URL' : 'Text';
                infoLength.textContent = content.length + ' characters';
                infoDate.textContent = new Date().toLocaleString();
                infoSize.textContent = size + 'x' + size + ' px';
                infoColors.textContent = `${color} on ${bgColor}`;
                
                QRCode.toCanvas(canvas, content, {
                    width: size,
                    color: {
                        dark: color,
                        light: bgColor
                    }
                }, function(error) {
                    if (error) {
                        console.error(error);
                        alert('Error generating QR code: ' + error.message);
                    } else {
                        downloadSection.style.display = 'block';
                    }
                });
            }
            
            generateBtn.addEventListener('click', generateQRCode);
            
            resetBtn.addEventListener('click', function() {
                qrContent.value = 'https://example.com';
                qrSize.value = '200';
                qrColor.value = '#000000';
                qrBgColor.value = '#ffffff';
                generateQRCode();
            });
            
            downloadBtn.addEventListener('click', function() {
                const link = document.createElement('a');
                link.download = 'qrcode.png';
                link.href = canvas.toDataURL('image/png');
                link.click();
            });
            
            qrSize.addEventListener('change', generateQRCode);
            qrColor.addEventListener('change', generateQRCode);
            qrBgColor.addEventListener('change', generateQRCode);
            
            generateQRCode();
        });

        // Global Chat Platform Script
        let replyingToMessage = null;

        function sendMessage() {
            const messageInput = document.getElementById("message-input");
            const chatBox = document.getElementById("chat-box");

            if (messageInput.value.trim() === "") return;

            const message = document.createElement("div");
            message.classList.add("message", "sent");
            message.innerHTML = replyingToMessage 
                ? `<div class='replying-to'>Replying to: ${replyingToMessage.innerText}</div>${messageInput.value}`
                : messageInput.value;

            const deleteButton = document.createElement("button");
            deleteButton.classList.add("delete-button");
            deleteButton.innerText = "X";
            deleteButton.onclick = function() {
                chatBox.removeChild(message);
            };
            message.appendChild(deleteButton);

            message.addEventListener("click", () => setReply(message));

            chatBox.appendChild(message);
            messageInput.value = "";
            replyingToMessage = null;
            document.getElementById("replying-to").style.display = "none";
        }

        function receiveMessage(text) {
            const chatBox = document.getElementById("chat-box");
            const message = document.createElement("div");
            message.classList.add("message", "received");
            message.innerHTML = text;

            const deleteButton = document.createElement("button");
            deleteButton.classList.add("delete-button");
            deleteButton.innerText = "X";
            deleteButton.onclick = function() {
                chatBox.removeChild(message);
            };
            message.appendChild(deleteButton);

            message.addEventListener("click", () => setReply(message));

            chatBox.appendChild(message);
        }

        function setReply(message) {
            replyingToMessage = message;
            document.getElementById("replying-to").innerText = "Replying to: " + message.innerText;
            document.getElementById("replying-to").style.display = "block";
        }

        function goBack() {
            document.getElementById("chat-section").style.display = "none";
        }

        // Choose Friend Section Script
        function openChooseFriend() {
            document.getElementById('choose-friend-section').style.display = 'block';
        }

        function closeChooseFriend() {
            document.getElementById('choose-friend-section').style.display = 'none';
        }

        function selectFriend(name, profilePic) {
            document.getElementById('user-name').innerText = name;
            document.getElementById('user-profile-pic').src = profilePic;
            closeChooseFriend();
            document.getElementById('chat-section').style.display = 'block';
        }

        // Simulate receiving a message
        setTimeout(() => receiveMessage("Hello! How are you?"), 2000);
    </script>
</body>
</html>
