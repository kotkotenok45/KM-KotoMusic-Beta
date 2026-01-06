<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KotoMusic Beta</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            color: #fff;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .player-container {
            width: 100%;
            max-width: 900px;
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.5);
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .player-header {
            background: rgba(0, 0, 0, 0.3);
            padding: 25px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo-icon {
            font-size: 28px;
            color: #6c5ce7;
        }

        .logo-text {
            font-size: 24px;
            font-weight: 700;
            letter-spacing: 1px;
            background: linear-gradient(90deg, #6c5ce7, #a29bfe);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .beta-badge {
            background: #6c5ce7;
            color: white;
            font-size: 12px;
            padding: 4px 10px;
            border-radius: 20px;
            font-weight: 600;
            margin-left: 5px;
        }

        .player-content {
            display: flex;
            min-height: 500px;
        }

        .player-sidebar {
            width: 35%;
            background: rgba(0, 0, 0, 0.2);
            padding: 25px;
            border-right: 1px solid rgba(255, 255, 255, 0.1);
            overflow-y: auto;
        }

        .player-main {
            width: 65%;
            padding: 30px;
            display: flex;
            flex-direction: column;
        }

        .now-playing {
            margin-bottom: 40px;
        }

        .now-playing-title {
            font-size: 14px;
            color: #a29bfe;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 10px;
        }

        .current-track {
            display: flex;
            align-items: center;
            gap: 20px;
            margin-bottom: 30px;
        }

        .album-art {
            width: 120px;
            height: 120px;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
            flex-shrink: 0;
        }

        .album-art img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .track-info {
            flex: 1;
        }

        .track-title {
            font-size: 22px;
            font-weight: 700;
            margin-bottom: 8px;
            color: #fff;
        }

        .track-artist {
            font-size: 16px;
            color: #a29bfe;
            margin-bottom: 5px;
        }

        .track-album {
            font-size: 14px;
            color: #aaa;
        }

        .player-controls {
            margin-top: auto;
        }

        .progress-area {
            margin-bottom: 25px;
        }

        .progress-bar {
            height: 6px;
            width: 100%;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            margin-bottom: 8px;
            cursor: pointer;
        }

        .progress {
            height: 100%;
            width: 0%;
            background: linear-gradient(90deg, #6c5ce7, #a29bfe);
            border-radius: 10px;
            position: relative;
        }

        .progress::after {
            content: '';
            position: absolute;
            height: 12px;
            width: 12px;
            border-radius: 50%;
            background: #fff;
            right: -5px;
            top: 50%;
            transform: translateY(-50%);
            box-shadow: 0 0 10px rgba(108, 92, 231, 0.8);
        }

        .timer {
            display: flex;
            justify-content: space-between;
            font-size: 14px;
            color: #aaa;
        }

        .controls {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 25px;
            margin-bottom: 20px;
        }

        .control-btn {
            background: transparent;
            border: none;
            color: #fff;
            font-size: 20px;
            cursor: pointer;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: all 0.3s;
        }

        .control-btn:hover {
            background: rgba(255, 255, 255, 0.1);
        }

        .play-pause {
            background: linear-gradient(135deg, #6c5ce7, #a29bfe);
            width: 60px;
            height: 60px;
            font-size: 24px;
            box-shadow: 0 5px 15px rgba(108, 92, 231, 0.4);
        }

        .play-pause:hover {
            transform: scale(1.05);
        }

        .volume-area {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-top: 20px;
        }

        .volume-icon {
            color: #a29bfe;
            font-size: 20px;
        }

        .volume-slider {
            flex: 1;
            height: 5px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            cursor: pointer;
        }

        .volume-percent {
            width: 70%;
            height: 100%;
            background: linear-gradient(90deg, #6c5ce7, #a29bfe);
            border-radius: 10px;
        }

        .playlist-title {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 20px;
            color: #fff;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .playlist-title i {
            color: #6c5ce7;
        }

        .playlist {
            list-style: none;
        }

        .playlist li {
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 15px;
            cursor: pointer;
            transition: all 0.3s;
            background: rgba(255, 255, 255, 0.05);
        }

        .playlist li:hover {
            background: rgba(255, 255, 255, 0.1);
        }

        .playlist li.active {
            background: rgba(108, 92, 231, 0.2);
            border-left: 4px solid #6c5ce7;
        }

        .playlist li .play-icon {
            color: #6c5ce7;
            font-size: 14px;
            opacity: 0.7;
        }

        .playlist li .track-details {
            flex: 1;
        }

        .playlist li .track-name {
            font-weight: 500;
            margin-bottom: 5px;
        }

        .playlist li .artist-name {
            font-size: 13px;
            color: #aaa;
        }

        .playlist li .track-duration {
            font-size: 14px;
            color: #aaa;
        }

        .visualizer {
            height: 100px;
            width: 100%;
            display: flex;
            align-items: flex-end;
            justify-content: center;
            gap: 3px;
            margin-bottom: 30px;
            padding: 0 10px;
        }

        .bar {
            width: 8px;
            background: linear-gradient(to top, #6c5ce7, #a29bfe);
            border-radius: 4px 4px 0 0;
            animation: equalizer 1.5s ease infinite alternate;
        }

        @keyframes equalizer {
            0% {
                height: 10%;
            }
            100% {
                height: 100%;
            }
        }

        .bar:nth-child(odd) {
            animation-delay: 0.5s;
        }

        .player-footer {
            padding: 20px 30px;
            background: rgba(0, 0, 0, 0.3);
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 14px;
            color: #aaa;
            text-align: center;
        }

        @media (max-width: 768px) {
            .player-content {
                flex-direction: column;
            }

            .player-sidebar, .player-main {
                width: 100%;
            }

            .player-sidebar {
                max-height: 300px;
            }
        }
    </style>
</head>
<body>
    <div class="player-container">
        <div class="player-header">
            <div class="logo">
                <i class="fas fa-music logo-icon"></i>
                <div class="logo-text">KotoMusic<span class="beta-badge">BETA</span></div>
            </div>
            <div class="player-status">
                <i class="fas fa-circle" style="color: #6c5ce7; font-size: 12px; margin-right: 8px;"></i>
                <span>Сейчас играет</span>
            </div>
        </div>
        
        <div class="player-content">
            <div class="player-main">
                <div class="now-playing">
                    <div class="now-playing-title">Сейчас играет</div>
                    <div class="current-track">
                        <div class="album-art">
                            <img src="https://images.unsplash.com/photo-1493225457124-a3eb161ffa5f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80" alt="Album Art">
                        </div>
                        <div class="track-info">
                            <div class="track-title">Midnight City</div>
                            <div class="track-artist">M83</div>
                            <div class="track-album">Hurry Up, We're Dreaming</div>
                        </div>
                    </div>
                </div>
                
                <div class="visualizer" id="visualizer">
                    <!-- Будет заполнено JavaScript -->
                </div>
                
                <div class="player-controls">
                    <div class="progress-area">
                        <div class="progress-bar" id="progress-bar">
                            <div class="progress" id="progress"></div>
                        </div>
                        <div class="timer">
                            <span class="current-time" id="current-time">0:00</span>
                            <span class="duration" id="duration">0:00</span>
                        </div>
                    </div>
                    
                    <div class="controls">
                        <button class="control-btn" id="prev-btn" title="Предыдущий трек">
                            <i class="fas fa-step-backward"></i>
                        </button>
                        <button class="control-btn play-pause" id="play-pause-btn" title="Воспроизвести/Пауза">
                            <i class="fas fa-play"></i>
                        </button>
                        <button class="control-btn" id="next-btn" title="Следующий трек">
                            <i class="fas fa-step-forward"></i>
                        </button>
                    </div>
                    
                    <div class="volume-area">
                        <i class="fas fa-volume-up volume-icon"></i>
                        <div class="volume-slider" id="volume-slider">
                            <div class="volume-percent" id="volume-percent"></div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="player-sidebar">
                <div class="playlist-title">
                    <i class="fas fa-list"></i> Плейлист
                </div>
                <ul class="playlist" id="playlist">
                    <!-- Плейлист будет заполнен JavaScript -->
                </ul>
            </div>
        </div>
        
        <div class="player-footer">
            KotoMusic Beta v1.0 | Для демонстрации используются треки из библиотеки Unsplash
        </div>
    </div>

    <audio id="audio-player"></audio>

    <script>
        // Данные плейлиста
        const playlistData = [
            {
                id: 1,
                title: "Midnight City",
                artist: "M83",
                album: "Hurry Up, We're Dreaming",
                duration: "4:04",
                cover: "https://images.unsplash.com/photo-1493225457124-a3eb161ffa5f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
                src: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3"
            },
            {
                id: 2,
                title: "Blinding Lights",
                artist: "The Weeknd",
                album: "After Hours",
                duration: "3:22",
                cover: "https://images.unsplash.com/photo-1511379938547-c1f69419868d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
                src: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3"
            },
            {
                id: 3,
                title: "Bohemian Rhapsody",
                artist: "Queen",
                album: "A Night at the Opera",
                duration: "5:55",
                cover: "https://images.unsplash.com/photo-1518609878373-06d740f60d8b?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
                src: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3"
            },
            {
                id: 4,
                title: "Take On Me",
                artist: "a-ha",
                album: "Hunting High and Low",
                duration: "3:47",
                cover: "https://images.unsplash.com/photo-1470225620780-dba8ba36b745?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
                src: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-4.mp3"
            },
            {
                id: 5,
                title: "Smells Like Teen Spirit",
                artist: "Nirvana",
                album: "Nevermind",
                duration: "5:01",
                cover: "https://images.unsplash.com/photo-1511671782779-c97d3d27a1d4?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
                src: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-5.mp3"
            },
            {
                id: 6,
                title: "Shape of You",
                artist: "Ed Sheeran",
                album: "÷ (Divide)",
                duration: "3:54",
                cover: "https://images.unsplash.com/photo-1511671782779-c97d3d27a1d4?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
                src: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-6.mp3"
            }
        ];

        // Инициализация элементов DOM
        const audioPlayer = document.getElementById('audio-player');
        const playPauseBtn = document.getElementById('play-pause-btn');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        const progressBar = document.getElementById('progress-bar');
        const progress = document.getElementById('progress');
        const currentTimeEl = document.getElementById('current-time');
        const durationEl = document.getElementById('duration');
        const volumeSlider = document.getElementById('volume-slider');
        const volumePercent = document.getElementById('volume-percent');
        const playlistEl = document.getElementById('playlist');
        const visualizer = document.getElementById('visualizer');
        
        // Текущий трек
        let currentTrackIndex = 0;
        let isPlaying = false;
        
        // Создание визуализатора
        function createVisualizer() {
            visualizer.innerHTML = '';
            for (let i = 0; i < 40; i++) {
                const bar = document.createElement('div');
                bar.className = 'bar';
                bar.style.animationDelay = `${i * 0.05}s`;
                bar.style.height = `${Math.random() * 80 + 20}%`;
                visualizer.appendChild(bar);
            }
        }
        
        // Загрузка плейлиста
        function loadPlaylist() {
            playlistData.forEach((track, index) => {
                const li = document.createElement('li');
                li.dataset.index = index;
                li.innerHTML = `
                    <i class="fas fa-play play-icon"></i>
                    <div class="track-details">
                        <div class="track-name">${track.title}</div>
                        <div class="artist-name">${track.artist}</div>
                    </div>
                    <div class="track-duration">${track.duration}</div>
                `;
                
                if (index === currentTrackIndex) {
                    li.classList.add('active');
                }
                
                li.addEventListener('click', () => {
                    loadTrack(index);
                    playTrack();
                });
                
                playlistEl.appendChild(li);
            });
        }
        
        // Загрузка трека
        function loadTrack(index) {
            currentTrackIndex = index;
            
            const track = playlistData[index];
            
            // Обновление информации о треке
            document.querySelector('.track-title').textContent = track.title;
            document.querySelector('.track-artist').textContent = track.artist;
            document.querySelector('.track-album').textContent = track.album;
            document.querySelector('.album-art img').src = track.cover;
            
            // Обновление аудио
            audioPlayer.src = track.src;
            
            // Обновление активного элемента в плейлисте
            document.querySelectorAll('.playlist li').forEach((li, i) => {
                if (i === index) {
                    li.classList.add('active');
                } else {
                    li.classList.remove('active');
                }
            });
            
            // Сброс прогресса
            progress.style.width = '0%';
            currentTimeEl.textContent = '0:00';
            
            // Когда аудио загружено, обновляем длительность
            audioPlayer.addEventListener('loadedmetadata', () => {
                durationEl.textContent = formatTime(audioPlayer.duration);
            });
        }
        
        // Воспроизведение трека
        function playTrack() {
            isPlaying = true;
            audioPlayer.play();
            playPauseBtn.innerHTML = '<i class="fas fa-pause"></i>';
            playPauseBtn.title = "Пауза";
            
            // Анимация визуализатора
            document.querySelectorAll('.bar').forEach(bar => {
                bar.style.animationPlayState = 'running';
            });
        }
        
        // Пауза трека
        function pauseTrack() {
            isPlaying = false;
            audioPlayer.pause();
            playPauseBtn.innerHTML = '<i class="fas fa-play"></i>';
            playPauseBtn.title = "Воспроизвести";
            
            // Остановка анимации визуализатора
            document.querySelectorAll('.bar').forEach(bar => {
                bar.style.animationPlayState = 'paused';
            });
        }
        
        // Форматирование времени в минуты:секунды
        function formatTime(seconds) {
            const min = Math.floor(seconds / 60);
            const sec = Math.floor(seconds % 60);
            return `${min}:${sec < 10 ? '0' : ''}${sec}`;
        }
        
        // Обновление прогресса
        function updateProgress(e) {
            const { duration, currentTime } = e.srcElement;
            const progressPercent = (currentTime / duration) * 100;
            progress.style.width = `${progressPercent}%`;
            currentTimeEl.textContent = formatTime(currentTime);
        }
        
        // Установка прогресса
        function setProgress(e) {
            const width = this.clientWidth;
            const clickX = e.offsetX;
            const duration = audioPlayer.duration;
            
            audioPlayer.currentTime = (clickX / width) * duration;
        }
        
        // Установка громкости
        function setVolume(e) {
            const width = this.clientWidth;
            const clickX = e.offsetX;
            const volume = clickX / width;
            
            audioPlayer.volume = volume;
            volumePercent.style.width = `${volume * 100}%`;
            
            // Обновление иконки громкости
            const volumeIcon = document.querySelector('.volume-icon');
            if (volume === 0) {
                volumeIcon.className = 'fas fa-volume-mute volume-icon';
            } else if (volume < 0.5) {
                volumeIcon.className = 'fas fa-volume-down volume-icon';
            } else {
                volumeIcon.className = 'fas fa-volume-up volume-icon';
            }
        }
        
        // Следующий трек
        function nextTrack() {
            currentTrackIndex++;
            if (currentTrackIndex >= playlistData.length) {
                currentTrackIndex = 0;
            }
            loadTrack(currentTrackIndex);
            if (isPlaying) {
                playTrack();
            }
        }
        
        // Предыдущий трек
        function prevTrack() {
            currentTrackIndex--;
            if (currentTrackIndex < 0) {
                currentTrackIndex = playlistData.length - 1;
            }
            loadTrack(currentTrackIndex);
            if (isPlaying) {
                playTrack();
            }
        }
        
        // Инициализация плеера
        function initPlayer() {
            createVisualizer();
            loadPlaylist();
            loadTrack(currentTrackIndex);
            
            // Установка громкости по умолчанию
            audioPlayer.volume = 0.7;
            volumePercent.style.width = '70%';
            
            // События аудио
            audioPlayer.addEventListener('timeupdate', updateProgress);
            audioPlayer.addEventListener('ended', nextTrack);
            
            // События кнопок
            playPauseBtn.addEventListener('click', () => {
                if (isPlaying) {
                    pauseTrack();
                } else {
                    playTrack();
                }
            });
            
            nextBtn.addEventListener('click', nextTrack);
            prevBtn.addEventListener('click', prevTrack);
            
            // События прогресса
            progressBar.addEventListener('click', setProgress);
            
            // События громкости
            volumeSlider.addEventListener('click', setVolume);
            
            // Горячие клавиши
            document.addEventListener('keydown', (e) => {
                switch(e.code) {
                    case 'Space':
                        e.preventDefault();
                        if (isPlaying) {
                            pauseTrack();
                        } else {
                            playTrack();
                        }
                        break;
                    case 'ArrowRight':
                        e.preventDefault();
                        nextTrack();
                        break;
                    case 'ArrowLeft':
                        e.preventDefault();
                        prevTrack();
                        break;
                    case 'ArrowUp':
                        e.preventDefault();
                        audioPlayer.volume = Math.min(audioPlayer.volume + 0.1, 1);
                        volumePercent.style.width = `${audioPlayer.volume * 100}%`;
                        break;
                    case 'ArrowDown':
                        e.preventDefault();
                        audioPlayer.volume = Math.max(audioPlayer.volume - 0.1, 0);
                        volumePercent.style.width = `${audioPlayer.volume * 100}%`;
                        break;
                }
            });
        }
        
        // Запуск плеера после загрузки страницы
        window.addEventListener('DOMContentLoaded', initPlayer);
    </script>
</body>
</html>
