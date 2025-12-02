<!DOCTYPE html>
<html lang="ms">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mood Booster</title>
    <style>
        body {
            background-color: #ffe4e1;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: sans-serif;
            text-align: center;
            overflow: hidden; /* Tambah ini untuk elak scrollbar semasa animasi */
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            max-width: 400px;
        }
        #pet-display {
            width: 150px; /* Saiz gambar */
            height: 150px;
            border-radius: 50%; /* Bentuk bulat untuk gambar */
            object-fit: cover; /* Pastikan gambar muat dalam bulatan */
            margin-bottom: 10px;
            border: 4px solid #ff69b4;
            /* Update transition untuk menampung pelbagai animasi */
            transition: transform 0.3s ease-out, border-color 0.5s, opacity 0.3s;
        }
        #status-message {
            margin-bottom: 10px;
            color: #ff69b4;
            font-weight: bold;
        }
        .buttons button {
            padding: 10px 15px;
            margin: 5px;
            font-size: 1em;
            cursor: pointer;
            background-color: #ff69b4;
            color: white;
            border: none;
            border-radius: 5px;
        }
        .meter {
            width: 100%;
            background-color: #f0f0f0;
            border-radius: 5px;
            margin-bottom: 10px;
        }
        .progress {
            width: 50%; /* Lebar awal */
            height: 20px;
            background-color: #ff1493; /* Warna merah jambu terang */
            border-radius: 5px;
            transition: width 0.5s ease-in-out;
            text-align: center;
            line-height: 20px;
            color: white;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Hi B (B for Brader)</h1>
        <!-- Gantikan 'my_image.png' dengan pautan gambar anda -->
        <img id="pet-display" src="ratna_normal.png" alt="Gambar Pet Maya">
        
        <div class="meter">
            <div id="health-bar" class="progress">Kesihatan</div>
        </div>
        
        <div id="status-message">Hai Anep!</div>
        <div class="buttons">
            <button onclick="feedPet()">Beri Makan 🍔</button>
            <button onclick="petPet()">Pujuk 🤗</button>
            <button onclick="sendKiss()">Send Kiss 😘</button>
        </div>
    </div>

<script>
    const petDisplay = document.getElementById('pet-display');
    const statusMessage = document.getElementById('status-message');
    const healthBar = document.getElementById('health-bar');

    // Status awal (skala 0 hingga 100)
    let health = 100;
    // Fungsi utiliti untuk tukar gambar
    function changeImage(imageSrc) {
        petDisplay.src = imageSrc;
    }

    // Fungsi apabila memberi makan
    function feedPet() {
        health = Math.min(100, health + 15);
        updatePetStatus("Yummy! Masyeh Anep! 😋");
        changeImage('ratna_makan.png'); // Tukar gambar makan
        // Animasi melantun kecil
        petDisplay.style.transform = 'translateY(-10px)'; 
        setTimeout(() => { petDisplay.style.transform = 'translateY(0px)'; }, 300);
    }

    // Fungsi apabila membelai
    function petPet() {
        health = Math.min(100, health + 10);
        updatePetStatus("Ocey, Tak Majuk Dah! 🥰");
        changeImage('ratna_gembira.png'); // Tukar gambar gembira
        // Animasi bergoncang (pusing)
        petDisplay.style.transform = 'rotate(-5deg)'; 
        setTimeout(() => {
            petDisplay.style.transform = 'rotate(5deg)';
            setTimeout(() => { petDisplay.style.transform = 'rotate(0deg)'; }, 100);
        }, 100);
    }

    // Fungsi baharu: Hantar Ciuman
    function sendKiss() {
        health = Math.min(100, health + 5); // Ciuman pun baik untuk kesihatan!
        updatePetStatus("Muaahh! 💖");
        changeImage('ratna_kiss.png'); // Tukar gambar cium
        // Animasi skala (zoom in/out)
        petDisplay.style.transform = 'scale(1.2)';
        petDisplay.style.borderColor = '#FF0000'; // Tukar border kepada merah cinta

        setTimeout(() => {
            petDisplay.style.transform = 'scale(1)';
            petDisplay.style.borderColor = '#ff69b4'; // Kembali ke warna asal
        }, 500);
    }

    // Fungsi untuk kemas kini paparan dan mesej
    function updatePetStatus(message) {
        statusMessage.textContent = message;
        healthBar.style.width = `${health}%`;
        healthBar.textContent = `${health}% Mood Titew`;
        
        if (health < 30) {
            statusMessage.style.color = 'red';
        } else {
            statusMessage.style.color = '#ff69b4';
        }
    } 

    /* FUNGSI animatePet() ASAL DIBUANG KERANA LOGIK BARU SUDAH DILETAKKAN DALAM FUNGSI INTERAKSI */

    // Kesihatan berkurangan secara beransur-ansur dari masa ke masa
    setInterval(() => {
        health = Math.max(0, health - 2);
        
        if (health === 0) {
            updatePetStatus("Oh No! Titew Rasa Tak Sihat Lah! 💀");
            changeImage('ratna_normal.png'); // Kembali ke gambar biasa bila tiada interaksi
        } else {
            updatePetStatus("Nak attention pwiss! 🥺"); 
            // Apabila berkurangan, kita tetapkan semula gambar kepada normal jika ia bukan normal
            if (!petDisplay.src.includes('ratna_normal.png') && 
                !petDisplay.src.includes('ratna_makan.png') && 
                !petDisplay.src.includes('ratna_gembira.png') && 
                !petDisplay.src.includes('ratna_kiss.png')) {
                    // Hanya tukar jika gambar semasa tiada dalam senarai interaksi aktif
                     changeImage('ratna_normal.png');
            }
        }

    }, 3000); // Setiap 3 saat

    // Muatkan status awal
    updatePetStatus("Hai Anep! Jaga Titew baik-baik ya! 😊");
    // Pastikan imej awal adalah normal
    changeImage('ratna_normal.png');

</script>
</body>
</html>
