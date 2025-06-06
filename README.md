# raj-movie
<!DOCTYPE html>
<html>
<head>
  <title>Raj Movie - Admin Panel</title>
  <script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-firestore.js"></script>
</head>
<body style="font-family: sans-serif;">
  <h2>Raj Movie 🎬 - Admin Upload Panel</h2>

  <form id="movieForm">
    <label>🎬 Movie Title:</label><br>
    <input type="text" id="title" required><br><br>

    <label>📝 Description:</label><br>
    <textarea id="description" required></textarea><br><br>

    <label>📅 Release Year:</label><br>
    <input type="number" id="year" required><br><br>

    <label>🖼 Thumbnail URL:</label><br>
    <input type="url" id="thumbnail" required><br><br>

    <label>🎥 Video URL (720p):</label><br>
    <input type="url" id="videoUrl" required><br><br>

    <button type="submit">📤 Upload Movie</button>
  </form>

  <p id="status"></p>

  <script>
    // ✅ তোমার Firebase Config
    const firebaseConfig = {
      apiKey: "AIzaSyCtIDXYXZ8qwrsYjhDulye7dKjNGypq6hg",
      authDomain: "raj-movie.firebaseapp.com",
      projectId: "raj-movie",
      storageBucket: "raj-movie.firebasestorage.app",
      messagingSenderId: "173216542976",
      appId: "1:173216542976:web:6a9a8713d2f23be36303e5",
      measurementId: "G-R2YXFNT2ST"
    };

    // Initialize Firebase
    const app = firebase.initializeApp(firebaseConfig);
    const db = firebase.firestore();

    // Submit Form
    document.getElementById('movieForm').addEventListener('submit', async (e) => {
      e.preventDefault();

      const title = document.getElementById('title').value;
      const description = document.getElementById('description').value;
      const year = parseInt(document.getElementById('year').value);
      const thumbnail = document.getElementById('thumbnail').value;
      const videoUrl = document.getElementById('videoUrl').value;

      try {
        await db.collection("movies").add({
          title,
          description,
          year,
          thumbnail,
          videoUrl
        });
        document.getElementById('status').innerText = "✅ Movie uploaded successfully!";
        document.getElementById('movieForm').reset();
      } catch (error) {
        console.error("❌ Error adding document: ", error);
        document.getElementById('status').innerText = "❌ Upload failed!";
      }
    });
  </script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Raj Movie - Admin Panel</title>
  <style>
    body {
      background: #000;
      color: #fff;
      font-family: Arial;
      padding: 20px;
    }
    input, textarea, button {
      display: block;
      margin: 10px 0;
      padding: 10px;
      width: 100%;
      max-width: 400px;
    }
    button {
      background-color: red;
      color: white;
      border: none;
    }
  </style>
</head>
<body>
  <h1>🎥 Raj Movie - Admin Panel</h1>

  <input type="text" id="title" placeholder="Movie Title">
  <input type="text" id="thumbnail" placeholder="Thumbnail Image URL">
  <input type="text" id="video" placeholder="Video URL (e.g. YouTube, Drive, etc)">
  <textarea id="description" placeholder="Movie Description"></textarea>
  <button onclick="uploadMovie()">Upload Movie</button>

  <p id="msg"></p>

  <!-- Firebase SDK -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
    import { getFirestore, collection, addDoc } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "AIzaSyCtIDXYXZ8qwrsYjhDulye7dKjNGypq6hg",
      authDomain: "raj-movie.firebaseapp.com",
      projectId: "raj-movie",
      storageBucket: "raj-movie.firebasestorage.app",
      messagingSenderId: "173216542976",
      appId: "1:173216542976:web:6a9a8713d2f23be36303e5",
      measurementId: "G-R2YXFNT2ST"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    window.uploadMovie = async function () {
      const title = document.getElementById("title").value;
      const thumbnail = document.getElementById("thumbnail").value;
      const video = document.getElementById("video").value;
      const description = document.getElementById("description").value;

      try {
        await addDoc(collection(db, "movies"), {
          title: title,
          thumbnail: thumbnail,
          video: video,
          description: description,
          timestamp: new Date()
        });
        document.getElementById("msg").innerText = "✅ Movie uploaded successfully!";
      } catch (e) {
        document.getElementById("msg").innerText = "❌ Upload failed: " + e.message;
      }
    }
  </script>
</body>
</html>