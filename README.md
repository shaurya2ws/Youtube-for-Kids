<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>YouTube-like Video, Like Button, Comment Section, View Count, Login/Guest Options, Subscribe, Sidebar Navigation with Search</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      flex-direction: column;
    }

    /* Search Bar Section */
    .search-bar-container {
      display: flex;
      justify-content: center;
      background-color: #f1f1f1;
      padding: 10px;
    }

    .search-bar {
      width: 50%;
      padding: 10px;
      font-size: 16px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    .create-btn {
      padding: 10px;
      margin-left: 10px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 16px;
      cursor: pointer;
    }

    /* Modal for Create Options */
    .modal {
      display: none;
      position: fixed;
      z-index: 1;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      overflow: auto;
      background-color: rgba(0, 0, 0, 0.4);
      padding-top: 60px;
    }

    .modal-content {
      background-color: #fefefe;
      margin: 5% auto;
      padding: 20px;
      border: 1px solid #888;
      width: 40%;
      border-radius: 8px;
      text-align: center;
    }

    .modal-header {
      font-size: 20px;
      margin-bottom: 15px;
    }

    .modal-option {
      padding: 10px;
      margin: 10px 0;
      font-size: 18px;
      cursor: pointer;
      border: 2px solid #007BFF;
      background-color: #ffffff;
      color: #007BFF;
      border-radius: 5px;
    }

    /* Sidebar Navigation */
    .sidebar {
      width: 200px;
      background-color: #333;
      position: fixed;
      top: 0;
      bottom: 0;
      left: 0;
      padding-top: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .sidebar a {
      color: white;
      padding: 14px;
      text-align: center;
      text-decoration: none;
      width: 100%;
      font-size: 18px;
      margin-bottom: 10px;
    }

    .sidebar a:hover {
      background-color: #575757;
    }

    .active {
      background-color: #4CAF50;
    }

    /* Main content section */
    .main-content {
      margin-left: 220px;
      padding: 20px;
      width: 100%;
    }

    /* Video Section */
    .video-container {
      width: 100%;
      max-width: 800px;
      margin: 20px auto;
      text-align: center;
    }

    .like-btn, .subscribe-btn {
      font-size: 18px;
      padding: 10px;
      cursor: pointer;
      border: 2px solid #007BFF;
      border-radius: 5px;
      background-color: #ffffff;
      color: #007BFF;
      display: inline-flex;
      align-items: center;
      margin-top: 10px;
    }

    .liked, .subscribed {
      color: #ff0000;
    }

    .comment-section {
      margin-top: 30px;
      width: 100%;
      max-width: 800px;
      margin-left: auto;
      margin-right: auto;
    }

    .comment-box {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      margin-bottom: 10px;
      font-size: 16px;
    }

    .submit-btn {
      padding: 10px;
      border: 2px solid #007BFF;
      background-color: #ffffff;
      color: #007BFF;
      cursor: pointer;
      border-radius: 5px;
      font-size: 16px;
    }

    .comment {
      padding: 10px;
      margin: 5px 0;
      background-color: #f8f8f8;
      border-radius: 5px;
    }

    .login-container {
      text-align: center;
      margin-top: 20px;
    }

    .login-btn, .guest-btn {
      padding: 10px;
      margin: 5px;
      cursor: pointer;
      border: 2px solid #007BFF;
      background-color: #ffffff;
      color: #007BFF;
      border-radius: 5px;
    }

    .view-count {
      font-size: 18px;
      margin-top: 10px;
      color: #007BFF;
    }

    .time-uploaded {
      font-size: 16px;
      margin-top: 5px;
      color: #555;
    }

  </style>
</head>
<body>

  <!-- Search Bar Section -->
  <div class="search-bar-container">
    <input type="text" id="search-bar" class="search-bar" placeholder="Search for videos, channels, or playlists">
    <button id="create-btn" class="create-btn">Create</button>
  </div>

  <!-- Sidebar Navigation -->
  <div class="sidebar">
    <a href="#" id="home-link" class="active">Home</a>
    <a href="#" id="shorts-link">Shorts</a>
    <a href="#" id="subscriptions-link">Subscriptions</a>
    <a href="#" id="you-link">You</a>
  </div>

  <!-- Main Content Section -->
  <div class="main-content">
    <!-- Login Section -->
    <div class="login-container">
      <button id="login-btn" class="login-btn">Login</button>
      <button id="guest-btn" class="guest-btn">Continue as Guest</button>
    </div>

    <!-- Video Section -->
    <div id="video-section" class="video-container">
      <video id="video" width="100%" controls>
        <source src="your-video-file.mp4" type="video/mp4">
        <!-- If you want to embed a YouTube video, you can use an iframe instead -->
        <!-- <iframe width="100%" height="400" src="https://www.youtube.com/embed/VIDEO_ID" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe> -->
        Your browser does not support the video tag.
      </video>

      <!-- Time Since Upload -->
      <div id="time-uploaded" class="time-uploaded"></div>

      <!-- Like Button Section -->
      <button id="like-button" class="like-btn">
        <span id="like-icon">&#128077;</span> <span id="like-count">0</span> Likes
      </button>

      <!-- Subscribe Button Section -->
      <button id="subscribe-button" class="subscribe-btn">
        Subscribe
      </button>

      <!-- View Count -->
      <div id="view-count" class="view-count">Views: 0</div>
    </div>

    <!-- Comment Section -->
    <div class="comment-section">
      <textarea id="comment-box" class="comment-box" placeholder="Write a comment..."></textarea><br>
      <button id="submit-comment" class="submit-btn">Submit Comment</button>

      <div id="comments-list"></div>
    </div>
  </div>

  <!-- Modal for Create Options -->
  <div id="create-modal" class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2>Create Something</h2>
      </div>
      <button class="modal-option" id="create-video">Create a Video</button>
      <button class="modal-option" id="upload-video">Upload a Video</button>
      <button class="modal-option" id="create-playlist">Create Playlist</button>
      <button class="modal-option" id="create-shorts">Create Shorts</button> <!-- New Option -->
    </div>
  </div>

  <script>
    // Variables
    let viewCount = localStorage.getItem("viewCount") ? parseInt(localStorage.getItem("viewCount")) : 0;
    let likeButton = document.getElementById('like-button');
    let likeIcon = document.getElementById('like-icon');
    let likeCount = document.getElementById('like-count');
    let count = 0;
    let liked = false;
    let commentBox = document.getElementById('comment-box');
    let commentsList = document.getElementById('comments-list');
    let submitCommentButton = document.getElementById('submit-comment');
    let viewCountDisplay = document.getElementById('view-count');
    let subscribeButton = document.getElementById('subscribe-button');
    let subscribed = false;

    // Create Modal
    let createBtn = document.getElementById('create-btn');
    let createModal = document.getElementById('create-modal');
    let createVideo = document.getElementById('create-video');
    let uploadVideo = document.getElementById('upload-video');
    let createPlaylist = document.getElementById('create-playlist');
    let createShorts = document.getElementById('create-shorts'); // New Button for Shorts

    createBtn.addEventListener('click', function() {
      createModal.style.display = 'block';
    });

    createVideo.addEventListener('click', function() {
      alert('Redirecting to create a video page...');
      createModal.style.display = 'none';
    });

    uploadVideo.addEventListener('click', function() {
      alert('Redirecting to upload a video page...');
      createModal.style.display = 'none';
    });

    createPlaylist.addEventListener('click', function() {
      alert('Redirecting to create a playlist...');
      createModal.style.display = 'none';
    });

    createShorts.addEventListener('click', function() {
      alert('Redirecting to create shorts...');
      createModal.style.display = 'none';
    });

    // Close modal when clicked outside
    window.onclick = function(event) {
      if (event.target == createModal) {
        createModal.style.display = 'none';
      }
    };

    // Video Upload Time (For demonstration, let's assume the video was uploaded 2 hours ago)
    let videoUploadTime = new Date();
    videoUploadTime.setHours(videoUploadTime.getHours() - 2); // Set upload time to 2 hours ago
    let timeUploadedDisplay = document.getElementById('time-uploaded');
    
    function updateTimeSinceUpload() {
      const now = new Date();
      const diffInMs = now - videoUploadTime;
      const diffInMinutes = Math.floor(diffInMs / (1000 * 60));

      let timeString;
      if (diffInMinutes < 60) {
        timeString = `${diffInMinutes} minutes ago`;
      } else if (diffInMinutes < 1440) {
        const hours = Math.floor(diffInMinutes / 60);
        timeString = `${hours} hour(s) ago`;
      } else {
        const days = Math.floor(diffInMinutes / 1440);
        timeString = `${days} day(s) ago`;
      }
      
      timeUploadedDisplay.textContent = `Uploaded ${timeString}`;
    }
    
    updateTimeSinceUpload(); // Initialize the time on page load

    // View count functionality
    viewCount++;
    localStorage.setItem("viewCount", viewCount);
    viewCountDisplay.textContent = `Views: ${viewCount}`;

    // Like Button Functionality
    likeButton.addEventListener('click', function() {
      liked = !liked;
      
      if (liked) {
        count++;
        likeButton.classList.add('liked');
      } else {
        count--;
        likeButton.classList.remove('liked');
      }

      likeCount.textContent = count;
    });

    // Subscribe Button Functionality
    subscribeButton.addEventListener('click', function() {
      subscribed = !subscribed;
      
      if (subscribed) {
        subscribeButton.classList.add('subscribed');
        subscribeButton.textContent = 'Unsubscribe';
        alert("You have subscribed!");
      } else {
        subscribeButton.classList.remove('subscribed');
        subscribeButton.textContent = 'Subscribe';
        alert("You have unsubscribed!");
      }
    });

    // Comment Section Functionality
    submitCommentButton.addEventListener('click', function() {
      const commentText = commentBox.value.trim();
      if (commentText) {
        const comment = document.createElement('div');
        comment.classList.add('comment');
        comment.textContent = commentText;
        commentsList.appendChild(comment);
        commentBox.value = ''; // Clear the comment box after submission
      }
    });
  </script>
</body>
</html>

