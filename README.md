<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Leo AI - Intelligent Study Platform</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background: #0f0f1a;
            color: #ffffff;
            overflow-x: hidden;
        }
        
        .font-display {
            font-family: 'Space Grotesk', sans-serif;
        }
        
        /* Animated Background */
        .bg-mesh {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: 
                radial-gradient(at 0% 0%, rgba(99, 102, 241, 0.15) 0px, transparent 50%),
                radial-gradient(at 100% 0%, rgba(168, 85, 247, 0.15) 0px, transparent 50%),
                radial-gradient(at 100% 100%, rgba(236, 72, 153, 0.15) 0px, transparent 50%),
                radial-gradient(at 0% 100%, rgba(59, 130, 246, 0.15) 0px, transparent 50%);
            animation: meshMove 20s ease-in-out infinite;
        }
        
        @keyframes meshMove {
            0%, 100% { transform: translate(0, 0) scale(1); }
            33% { transform: translate(30px, -30px) scale(1.1); }
            66% { transform: translate(-20px, 20px) scale(0.9); }
        }
        
        /* Glassmorphism */
        .glass {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
        }
        
        .glass-strong {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(30px);
            border: 1px solid rgba(255, 255, 255, 0.15);
        }
        
        /* Gradient Text */
        .gradient-text {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .gradient-text-cyan {
            background: linear-gradient(135deg, #06b6d4 0%, #3b82f6 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        /* Interactive Cards */
        .study-card {
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            transform-style: preserve-3d;
        }
        
        .study-card:hover {
            transform: translateY(-8px) rotateX(5deg);
            box-shadow: 0 20px 40px rgba(99, 102, 241, 0.3);
        }
        
        /* Flashcard Flip */
        .flashcard-container {
            perspective: 1000px;
        }
        
        .flashcard {
            position: relative;
            width: 100%;
            height: 300px;
            transform-style: preserve-3d;
            transition: transform 0.6s;
            cursor: pointer;
        }
        
        .flashcard.flipped {
            transform: rotateY(180deg);
        }
        
        .flashcard-face {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            border-radius: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 2rem;
            text-align: center;
        }
        
        .flashcard-front {
            background: linear-gradient(135deg, rgba(99, 102, 241, 0.2), rgba(168, 85, 247, 0.2));
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .flashcard-back {
            background: linear-gradient(135deg, rgba(59, 130, 246, 0.2), rgba(147, 51, 234, 0.2));
            border: 1px solid rgba(255, 255, 255, 0.1);
            transform: rotateY(180deg);
        }
        
        /* Progress Ring */
        .progress-ring {
            transform: rotate(-90deg);
        }
        
        .progress-ring-circle {
            transition: stroke-dashoffset 0.5s ease-in-out;
        }
        
        /* Typing Animation */
        .typing-dot {
            animation: typing 1.4s infinite;
        }
        
        .typing-dot:nth-child(2) { animation-delay: 0.2s; }
        .typing-dot:nth-child(3) { animation-delay: 0.4s; }
        
        @keyframes typing {
            0%, 60%, 100% { transform: translateY(0); }
            30% { transform: translateY(-10px); }
        }
        
        /* Floating Elements */
        .float {
            animation: float 6s ease-in-out infinite;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }
        
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        
        ::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.05);
        }
        
        ::-webkit-scrollbar-thumb {
            background: rgba(99, 102, 241, 0.5);
            border-radius: 4px;
        }
        
        /* Tab Animation */
        .tab-active {
            background: linear-gradient(135deg, rgba(99, 102, 241, 0.3), rgba(168, 85, 247, 0.3));
            border: 1px solid rgba(99, 102, 241, 0.5);
        }
        
        /* Input Glow */
        .input-glow:focus {
            box-shadow: 0 0 20px rgba(99, 102, 241, 0.5);
            border-color: rgba(99, 102, 241, 0.8);
        }
        
        /* Pulse Animation for AI */
        .ai-pulse {
            animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: .5; }
        }
        
        /* Confetti */
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background: #f0f;
            animation: confetti-fall 3s linear forwards;
        }
        
        @keyframes confetti-fall {
            to {
                transform: translateY(100vh) rotate(720deg);
                opacity: 0;
            }
        }
        
        /* Chat Message */
        .chat-message {
            animation: slideIn 0.3s ease-out;
        }
        
        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        /* Quiz Option */
        .quiz-option {
            transition: all 0.3s ease;
        }
        
        .quiz-option:hover {
            background: rgba(99, 102, 241, 0.2);
            transform: translateX(10px);
        }
        
        .quiz-option.correct {
            background: rgba(34, 197, 94, 0.3);
            border-color: rgba(34, 197, 94, 0.5);
        }
        
        .quiz-option.wrong {
            background: rgba(239, 68, 68, 0.3);
            border-color: rgba(239, 68, 68, 0.5);
        }
    </style>
</head>
<body class="antialiased">
    <div class="bg-mesh"></div>
    
    <!-- Navigation -->
    <nav class="fixed top-0 w-full z-50 glass-strong border-b border-white/10">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16">
                <div class="flex items-center space-x-3">
                    <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-indigo-500 to-purple-600 flex items-center justify-center">
                        <i data-lucide="brain" class="w-6 h-6 text-white"></i>
                    </div>
                    <span class="font-display text-xl font-bold gradient-text">Leo AI</span>
                </div>
                
                <div class="hidden md:flex items-center space-x-8">
                    <a href="#features" class="text-sm font-medium text-gray-300 hover:text-white transition">Features</a>
                    <a href="#upload" class="text-sm font-medium text-gray-300 hover:text-white transition">Create</a>
                    <a href="#study" class="text-sm font-medium text-gray-300 hover:text-white transition">Study</a>
                    <button class="px-4 py-2 rounded-lg bg-white/10 hover:bg-white/20 transition text-sm font-medium border border-white/10">
                        Sign In
                    </button>
                    <button class="px-4 py-2 rounded-lg bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-500 hover:to-purple-500 transition text-sm font-medium shadow-lg shadow-indigo-500/30">
                        Get Started
                    </button>
                </div>
                
                <button class="md:hidden p-2" onclick="toggleMobileMenu()">
                    <i data-lucide="menu" class="w-6 h-6"></i>
                </button>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section class="relative pt-32 pb-20 px-4 sm:px-6 lg:px-8 overflow-hidden">
        <div class="max-w-7xl mx-auto">
            <div class="text-center mb-16">
                <div class="inline-flex items-center px-4 py-2 rounded-full glass mb-6 float">
                    <span class="flex h-2 w-2 rounded-full bg-green-400 mr-2"></span>
                    <span class="text-sm font-medium text-gray-300">AI-Powered Learning</span>
                </div>
                
                <h1 class="font-display text-5xl md:text-7xl font-bold mb-6 leading-tight">
                    Study Less. <span class="gradient-text">Learn More.</span><br>
                    Ace Every Exam.
                </h1>
                
                <p class="text-xl text-gray-400 max-w-2xl mx-auto mb-10">
                    Transform any PDF, video, or lecture into beautiful notes, flashcards, and quizzes instantly. 
                    Your personal AI tutor available 24/7.
                </p>
                
                <div class="flex flex-col sm:flex-row gap-4 justify-center">
                    <button onclick="scrollToUpload()" class="px-8 py-4 rounded-xl bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-500 hover:to-purple-500 transition font-semibold text-lg shadow-xl shadow-indigo-500/30 flex items-center justify-center gap-2 group">
                        <span>Start Learning Now</span>
                        <i data-lucide="arrow-right" class="w-5 h-5 group-hover:translate-x-1 transition"></i>
                    </button>
                    <button class="px-8 py-4 rounded-xl glass hover:bg-white/10 transition font-semibold text-lg flex items-center justify-center gap-2">
                        <i data-lucide="play-circle" class="w-5 h-5"></i>
                        <span>Watch Demo</span>
                    </button>
                </div>
            </div>

            <!-- Stats -->
            <div class="grid grid-cols-2 md:grid-cols-4 gap-6 max-w-4xl mx-auto mb-20">
                <div class="glass rounded-2xl p-6 text-center">
                    <div class="text-3xl font-bold gradient-text-cyan mb-1">5M+</div>
                    <div class="text-sm text-gray-400">Students</div>
                </div>
                <div class="glass rounded-2xl p-6 text-center">
                    <div class="text-3xl font-bold gradient-text mb-1">15M+</div>
                    <div class="text-sm text-gray-400">Notes Generated</div>
                </div>
                <div class="glass rounded-2xl p-6 text-center">
                    <div class="text-3xl font-bold text-green-400 mb-1">95%</div>
                    <div class="text-sm text-gray-400">Retention Rate</div>
                </div>
                <div class="glass rounded-2xl p-6 text-center">
                    <div class="text-3xl font-bold text-purple-400 mb-1">4.9★</div>
                    <div class="text-sm text-gray-400">User Rating</div>
                </div>
            </div>
        </div>
    </section>

    <!-- Main App Interface -->
    <section id="upload" class="py-20 px-4 sm:px-6 lg:px-8">
        <div class="max-w-7xl mx-auto">
            <div class="glass rounded-3xl p-8 md:p-12 mb-12">
                <div class="text-center mb-10">
                    <h2 class="font-display text-3xl md:text-4xl font-bold mb-4">Create Your Study Materials</h2>
                    <p class="text-gray-400">Upload any content and let Leo AI transform it into comprehensive study tools</p>
                </div>

                <!-- Upload Tabs -->
                <div class="flex flex-wrap justify-center gap-2 mb-8">
                    <button onclick="switchTab('pdf')" id="tab-pdf" class="tab-active px-6 py-3 rounded-xl font-medium transition flex items-center gap-2">
                        <i data-lucide="file-text" class="w-5 h-5"></i>
                        <span>PDF / Document</span>
                    </button>
                    <button onclick="switchTab('video')" id="tab-video" class="px-6 py-3 rounded-xl font-medium text-gray-400 hover:text-white transition flex items-center gap-2 bg-white/5">
                        <i data-lucide="video" class="w-5 h-5"></i>
                        <span>YouTube / Video</span>
                    </button>
                    <button onclick="switchTab('audio')" id="tab-audio" class="px-6 py-3 rounded-xl font-medium text-gray-400 hover:text-white transition flex items-center gap-2 bg-white/5">
                        <i data-lucide="mic" class="w-5 h-5"></i>
                        <span>Record Lecture</span>
                    </button>
                    <button onclick="switchTab('text')" id="tab-text" class="px-6 py-3 rounded-xl font-medium text-gray-400 hover:text-white transition flex items-center gap-2 bg-white/5">
                        <i data-lucide="type" class="w-5 h-5"></i>
                        <span>Paste Text</span>
                    </button>
                </div>

                <!-- Upload Area -->
                <div id="upload-area" class="border-2 border-dashed border-white/20 rounded-2xl p-12 text-center hover:border-indigo-500/50 transition cursor-pointer bg-white/5 backdrop-blur-sm relative overflow-hidden group" ondrop="handleDrop(event)" ondragover="handleDragOver(event)" onclick="document.getElementById('file-input').click()">
                    <input type="file" id="file-input" class="hidden" accept=".pdf,.doc,.docx,.txt" onchange="handleFileSelect(event)">
                    
                    <div class="absolute inset-0 bg-gradient-to-r from-indigo-600/0 via-indigo-600/10 to-purple-600/0 translate-x-[-100%] group-hover:translate-x-[100%] transition-transform duration-1000"></div>
                    
                    <div class="relative z-10">
                        <div class="w-20 h-20 rounded-2xl bg-gradient-to-br from-indigo-500/20 to-purple-500/20 flex items-center justify-center mx-auto mb-6 group-hover:scale-110 transition">
                            <i data-lucide="upload-cloud" class="w-10 h-10 text-indigo-400"></i>
                        </div>
                        <h3 class="text-xl font-semibold mb-2">Drop your files here</h3>
                        <p class="text-gray-400 mb-4">or click to browse (PDF, DOCX, TXT up to 50MB)</p>
                        <div class="flex justify-center gap-2 text-sm text-gray-500">
                            <span class="flex items-center gap-1"><i data-lucide="zap" class="w-4 h-4"></i> Instant processing</span>
                            <span class="flex items-center gap-1"><i data-lucide="shield" class="w-4 h-4"></i> Secure & private</span>
                        </div>
                    </div>
                </div>

                <!-- URL Input (for video) -->
                <div id="url-input-area" class="hidden">
                    <div class="flex gap-4">
                        <input type="text" placeholder="Paste YouTube URL here..." class="flex-1 px-6 py-4 rounded-xl bg-white/5 border border-white/10 focus:outline-none input-glow text-white placeholder-gray-500">
                        <button onclick="processURL()" class="px-8 py-4 rounded-xl bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-500 hover:to-purple-500 transition font-semibold flex items-center gap-2">
                            <i data-lucide="wand-2" class="w-5 h-5"></i>
                            <span>Generate</span>
                        </button>
                    </div>
                </div>

                <!-- Recording Interface -->
                <div id="recording-area" class="hidden text-center py-12">
                    <div class="w-32 h-32 rounded-full bg-red-500/20 flex items-center justify-center mx-auto mb-6 relative cursor-pointer" onclick="toggleRecording()" id="record-btn">
                        <div class="absolute inset-0 rounded-full bg-red-500/30 animate-ping"></div>
                        <i data-lucide="mic" class="w-12 h-12 text-red-400 relative z-10"></i>
                    </div>
                    <p class="text-xl font-semibold mb-2" id="recording-status">Click to start recording</p>
                    <p class="text-gray-400">Record your lecture and convert to notes instantly</p>
                    <div id="recording-timer" class="mt-4 text-3xl font-mono font-bold hidden">00:00</div>
                </div>

                <!-- Text Input -->
                <div id="text-input-area" class="hidden">
                    <textarea placeholder="Paste your lecture notes, article text, or any content here..." rows="8" class="w-full px-6 py-4 rounded-xl bg-white/5 border border-white/10 focus:outline-none input-glow text-white placeholder-gray-500 resize-none mb-4"></textarea>
                    <button onclick="processText()" class="w-full px-8 py-4 rounded-xl bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-500 hover:to-purple-500 transition font-semibold flex items-center justify-center gap-2">
                        <i data-lucide="sparkles" class="w-5 h-5"></i>
                        <span>Generate Study Materials</span>
                    </button>
                </div>

                <!-- Processing Animation -->
                <div id="processing" class="hidden py-12 text-center">
                    <div class="relative w-24 h-24 mx-auto mb-6">
                        <div class="absolute inset-0 rounded-full border-4 border-indigo-500/30"></div>
                        <div class="absolute inset-0 rounded-full border-4 border-indigo-500 border-t-transparent animate-spin"></div>
                        <div class="absolute inset-0 flex items-center justify-center">
                            <i data-lucide="brain" class="w-10 h-10 text-indigo-400 ai-pulse"></i>
                        </div>
                    </div>
                    <h3 class="text-xl font-semibold mb-2">Leo AI is analyzing your content...</h3>
                    <p class="text-gray-400" id="processing-step">Extracting key concepts...</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Study Dashboard (Hidden initially) -->
    <section id="study" class="hidden py-12 px-4 sm:px-6 lg:px-8">
        <div class="max-w-7xl mx-auto">
            <!-- Study Header -->
            <div class="glass rounded-2xl p-6 mb-8 flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                <div>
                    <h2 class="font-display text-2xl font-bold mb-1" id="study-title">Operating Systems: Crash Course CS #18</h2>
                    <p class="text-sm text-gray-400">Generated 2 minutes ago • 12 min read</p>
                </div>
                <div class="flex gap-3">
                    <button onclick="exportContent('pdf')" class="px-4 py-2 rounded-lg glass hover:bg-white/10 transition text-sm font-medium flex items-center gap-2">
                        <i data-lucide="download" class="w-4 h-4"></i>
                        <span>Export PDF</span>
                    </button>
                    <button onclick="shareContent()" class="px-4 py-2 rounded-lg glass hover:bg-white/10 transition text-sm font-medium flex items-center gap-2">
                        <i data-lucide="share-2" class="w-4 h-4"></i>
                        <span>Share</span>
                    </button>
                </div>
            </div>

            <!-- Study Modes Navigation -->
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-8">
                <button onclick="switchStudyMode('notes')" id="mode-notes" class="study-card glass rounded-2xl p-6 text-left tab-active">
                    <div class="w-12 h-12 rounded-xl bg-indigo-500/20 flex items-center justify-center mb-4">
                        <i data-lucide="file-text" class="w-6 h-6 text-indigo-400"></i>
                    </div>
                    <h3 class="font-semibold mb-1">Smart Notes</h3>
                    <p class="text-sm text-gray-400">AI-generated summary</p>
                </button>
                
                <button onclick="switchStudyMode('flashcards')" id="mode-flashcards" class="study-card glass rounded-2xl p-6 text-left bg-white/5">
                    <div class="w-12 h-12 rounded-xl bg-purple-500/20 flex items-center justify-center mb-4">
                        <i data-lucide="layers" class="w-6 h-6 text-purple-400"></i>
                    </div>
                    <h3 class="font-semibold mb-1">Flashcards</h3>
                    <p class="text-sm text-gray-400">24 cards generated</p>
                </button>
                
                <button onclick="switchStudyMode('quiz')" id="mode-quiz" class="study-card glass rounded-2xl p-6 text-left bg-white/5">
                    <div class="w-12 h-12 rounded-xl bg-pink-500/20 flex items-center justify-center mb-4">
                        <i data-lucide="help-circle" class="w-6 h-6 text-pink-400"></i>
                    </div>
                    <h3 class="font-semibold mb-1">Practice Quiz</h3>
                    <p class="text-sm text-gray-400">Test your knowledge</p>
                </button>
                
                <button onclick="switchStudyMode('chat')" id="mode-chat" class="study-card glass rounded-2xl p-6 text-left bg-white/5">
                    <div class="w-12 h-12 rounded-xl bg-cyan-500/20 flex items-center justify-center mb-4">
                        <i data-lucide="message-square" class="w-6 h-6 text-cyan-400"></i>
                    </div>
                    <h3 class="font-semibold mb-1">AI Tutor</h3>
                    <p class="text-sm text-gray-400">Ask anything</p>
                </button>
            </div>

            <!-- Content Areas -->
            
            <!-- Notes View -->
            <div id="view-notes" class="glass rounded-2xl p-8">
                <div class="prose prose-invert max-w-none">
                    <div class="flex items-center justify-between mb-6">
                        <h3 class="text-2xl font-bold gradient-text">Study Notes: Operating Systems</h3>
                        <div class="flex gap-2">
                            <button onclick="toggleEdit()" class="px-3 py-1 rounded-lg bg-white/10 hover:bg-white/20 transition text-sm">
                                <i data-lucide="edit-3" class="w-4 h-4 inline mr-1"></i> Edit
                            </button>
                        </div>
                    </div>
                    
                    <div id="notes-content" class="space-y-6 text-gray-300 leading-relaxed">
                        <div class="p-4 rounded-xl bg-indigo-500/10 border border-indigo-500/20">
                            <h4 class="text-lg font-semibold text-indigo-300 mb-2">🎯 Overview</h4>
                            <p>Operating systems act as the "playground monitor" of computers, managing hardware resources and providing abstractions that make computers usable.</p>
                        </div>

                        <div class="grid md:grid-cols-2 gap-4">
                            <div class="p-4 rounded-xl bg-white/5 border border-white/10">
                                <h4 class="font-semibold text-purple-300 mb-2">📚 Historical Context</h4>
                                <ul class="list-disc list-inside space-y-1 text-sm">
                                    <li>1940s: Manual operation, one program at a time</li>
                                    <li>1950s: Batch processing introduced</li>
                                    <li>1960s: Time-sharing and multitasking</li>
                                    <li>Modern: Protected memory, virtual memory</li>
                                </ul>
                            </div>
                            
                            <div class="p-4 rounded-xl bg-white/5 border border-white/10">
                                <h4 class="font-semibold text-cyan-300 mb-2">⚙️ Core Functions</h4>
                                <ul class="list-disc list-inside space-y-1 text-sm">
                                    <li>CPU Management & Scheduling</li>
                                    <li>Memory Management</li>
                                    <li>Device Driver Management</li>
                                    <li>File System & Storage</li>
                                </ul>
                            </div>
                        </div>

                        <div class="p-4 rounded-xl bg-white/5 border border-white/10">
                            <h4 class="font-semibold text-pink-300 mb-3">🧠 Key Concepts</h4>
                            
                            <div class="space-y-3">
                                <div class="border-l-2 border-indigo-500 pl-4">
                                    <h5 class="font-medium text-white">Multitasking</h5>
                                    <p class="text-sm">The ability to run multiple programs seemingly simultaneously through rapid context switching.</p>
                                </div>
                                
                                <div class="border-l-2 border-purple-500 pl-4">
                                    <h5 class="font-medium text-white">Virtual Memory</h5>
                                    <p class="text-sm">Abstraction that gives each program its own memory space, isolating processes for security and stability.</p>
                                </div>
                                
                                <div class="border-l-2 border-cyan-500 pl-4">
                                    <h5 class="font-medium text-white">The Kernel</h5>
                                    <p class="text-sm">Core OS component with full hardware access, always resident in memory, managing system calls.</p>
                                </div>
                            </div>
                        </div>

                        <div class="p-4 rounded-xl bg-yellow-500/10 border border-yellow-500/20">
                            <h4 class="font-semibold text-yellow-300 mb-2">💡 Memory Management Techniques</h4>
                            <p class="mb-2"><strong>Paging:</strong> Divides memory into fixed-size blocks (pages), allows non-contiguous physical memory allocation.</p>
                            <p><strong>Segmentation:</strong> Variable-sized blocks matching logical program structure.</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Flashcards View -->
            <div id="view-flashcards" class="hidden">
                <div class="flex justify-between items-center mb-6">
                    <div>
                        <h3 class="text-2xl font-bold">Flashcards</h3>
                        <p class="text-gray-400 text-sm">Click cards to flip • Use arrows to navigate</p>
                    </div>
                    <div class="flex items-center gap-4">
                        <div class="text-sm text-gray-400">
                            Card <span id="card-current" class="text-white font-bold">1</span> of <span id="card-total">6</span>
                        </div>
                        <div class="flex gap-2">
                            <button onclick="prevCard()" class="p-2 rounded-lg glass hover:bg-white/10 transition">
                                <i data-lucide="chevron-left" class="w-5 h-5"></i>
                            </button>
                            <button onclick="nextCard()" class="p-2 rounded-lg glass hover:bg-white/10 transition">
                                <i data-lucide="chevron-right" class="w-5 h-5"></i>
                            </button>
                        </div>
                    </div>
                </div>

                <div class="flashcard-container max-w-2xl mx-auto mb-8">
                    <div id="flashcard" class="flashcard" onclick="flipCard()">
                        <div class="flashcard-face flashcard-front">
                            <div>
                                <div class="text-sm text-indigo-300 mb-4 uppercase tracking-wider">Question</div>
                                <h4 class="text-2xl font-semibold" id="card-question">What is the primary role of an Operating System?</h4>
                            </div>
                        </div>
                        <div class="flashcard-face flashcard-back">
                            <div>
                                <div class="text-sm text-cyan-300 mb-4 uppercase tracking-wider">Answer</div>
                                <p class="text-xl" id="card-answer">To act as a "playground monitor" managing hardware resources (CPU, memory, devices) and providing abstractions that make computers usable for programmers and users.</p>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="flex justify-center gap-4">
                    <button onclick="markDifficult()" class="px-6 py-3 rounded-xl bg-red-500/20 hover:bg-red-500/30 text-red-300 transition flex items-center gap-2">
                        <i data-lucide="x-circle" class="w-5 h-5"></i>
                        <span>Difficult</span>
                    </button>
                    <button onclick="markEasy()" class="px-6 py-3 rounded-xl bg-green-500/20 hover:bg-green-500/30 text-green-300 transition flex items-center gap-2">
                        <i data-lucide="check-circle" class="w-5 h-5"></i>
                        <span>Got it!</span>
                    </button>
                </div>

                <!-- Progress -->
                <div class="max-w-2xl mx-auto mt-8">
                    <div class="flex justify-between text-sm mb-2">
                        <span class="text-gray-400">Study Progress</span>
                        <span class="text-white" id="progress-text">0% Mastered</span>
                    </div>
                    <div class="h-2 rounded-full bg-white/10 overflow-hidden">
                        <div id="progress-bar" class="h-full bg-gradient-to-r from-indigo-500 to-purple-500 transition-all duration-500" style="width: 0%"></div>
                    </div>
                </div>
            </div>

            <!-- Quiz View -->
            <div id="view-quiz" class="hidden glass rounded-2xl p-8">
                <div class="max-w-3xl mx-auto">
                    <div class="flex justify-between items-center mb-8">
                        <h3 class="text-2xl font-bold">Practice Quiz</h3>
                        <div class="flex items-center gap-2">
                            <span class="text-sm text-gray-400">Score:</span>
                            <span id="quiz-score" class="text-2xl font-bold gradient-text">0/0</span>
                        </div>
                    </div>

                    <div id="quiz-container">
                        <div class="mb-6">
                            <div class="text-sm text-indigo-400 mb-2 font-medium">Question <span id="q-number">1</span> of 5</div>
                            <h4 class="text-xl font-semibold mb-6" id="q-text">Which component of the OS has full hardware access and remains resident in memory?</h4>
                            
                            <div class="space-y-3" id="q-options">
                                <button onclick="selectAnswer(0)" class="quiz-option w-full p-4 rounded-xl glass text-left hover:bg-white/10 transition flex items-center gap-3">
                                    <div class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center font-semibold text-sm">A</div>
                                    <span>Device Driver</span>
                                </button>
                                <button onclick="selectAnswer(1)" class="quiz-option w-full p-4 rounded-xl glass text-left hover:bg-white/10 transition flex items-center gap-3">
                                    <div class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center font-semibold text-sm">B</div>
                                    <span>The Kernel</span>
                                </button>
                                <button onclick="selectAnswer(2)" class="quiz-option w-full p-4 rounded-xl glass text-left hover:bg-white/10 transition flex items-center gap-3">
                                    <div class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center font-semibold text-sm">C</div>
                                    <span>File System</span>
                                </button>
                                <button onclick="selectAnswer(3)" class="quiz-option w-full p-4 rounded-xl glass text-left hover:bg-white/10 transition flex items-center gap-3">
                                    <div class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center font-semibold text-sm">D</div>
                                    <span>Virtual Memory Manager</span>
                                </button>
                            </div>
                        </div>

                        <div id="quiz-feedback" class="hidden mb-6 p-4 rounded-xl bg-white/5 border border-white/10">
                            <div class="flex items-start gap-3">
                                <div id="feedback-icon" class="w-6 h-6 rounded-full flex items-center justify-center mt-0.5"></div>
                                <div>
                                    <h5 class="font-semibold mb-1" id="feedback-title"></h5>
                                    <p class="text-sm text-gray-400" id="feedback-text"></p>
                                </div>
                            </div>
                        </div>

                        <button id="next-q-btn" onclick="nextQuestion()" class="hidden w-full py-3 rounded-xl bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-500 hover:to-purple-500 transition font-semibold">
                            Next Question
                        </button>
                    </div>

                    <div id="quiz-complete" class="hidden text-center py-12">
                        <div class="w-24 h-24 rounded-full bg-gradient-to-br from-green-400 to-emerald-600 flex items-center justify-center mx-auto mb-6">
                            <i data-lucide="trophy" class="w-12 h-12 text-white"></i>
                        </div>
                        <h3 class="text-3xl font-bold mb-2">Quiz Complete!</h3>
                        <p class="text-gray-400 mb-6">You scored <span id="final-score" class="text-white font-bold"></span></p>
                        <div class="flex justify-center gap-4">
                            <button onclick="restartQuiz()" class="px-6 py-3 rounded-xl glass hover:bg-white/10 transition">Try Again</button>
                            <button onclick="switchStudyMode('flashcards')" class="px-6 py-3 rounded-xl bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-500 hover:to-purple-500 transition">Review Flashcards</button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- AI Tutor Chat -->
            <div id="view-chat" class="hidden glass rounded-2xl overflow-hidden flex flex-col h-[600px]">
                <div class="p-4 border-b border-white/10 bg-white/5 flex justify-between items-center">
                    <div class="flex items-center gap-3">
                        <div class="w-10 h-10 rounded-full bg-gradient-to-br from-cyan-500 to-blue-600 flex items-center justify-center">
                            <i data-lucide="bot" class="w-5 h-5 text-white"></i>
                        </div>
                        <div>
                            <h4 class="font-semibold">Leo AI Tutor</h4>
                            <p class="text-xs text-green-400 flex items-center gap-1">
                                <span class="w-2 h-2 rounded-full bg-green-400"></span>
                                Online
                            </p>
                        </div>
                    </div>
                    <button onclick="clearChat()" class="p-2 rounded-lg hover:bg-white/10 transition">
                        <i data-lucide="trash-2" class="w-5 h-5 text-gray-400"></i>
                    </button>
                </div>

                <div id="chat-messages" class="flex-1 overflow-y-auto p-4 space-y-4">
                    <div class="chat-message flex gap-3">
                        <div class="w-8 h-8 rounded-full bg-gradient-to-br from-cyan-500 to-blue-600 flex-shrink-0 flex items-center justify-center">
                            <i data-lucide="bot" class="w-4 h-4 text-white"></i>
                        </div>
                        <div class="glass rounded-2xl rounded-tl-none p-4 max-w-[80%]">
                            <p class="text-sm">Hi! I'm Leo, your AI tutor for Operating Systems. I've analyzed your study materials and I'm ready to help! Ask me anything about the content. 👋</p>
                        </div>
                    </div>
                </div>

                <div class="p-4 border-t border-white/10 bg-white/5">
                    <div class="flex gap-2 mb-3 overflow-x-auto pb-2">
                        <button onclick="quickAsk('What is virtual memory?')" class="px-3 py-1 rounded-full bg-white/10 hover:bg-white/20 transition text-xs whitespace-nowrap">What is virtual memory?</button>
                        <button onclick="quickAsk('Explain the kernel')" class="px-3 py-1 rounded-full bg-white/10 hover:bg-white/20 transition text-xs whitespace-nowrap">Explain the kernel</button>
                        <button onclick="quickAsk('Difference between paging and segmentation?')" class="px-3 py-1 rounded-full bg-white/10 hover:bg-white/20 transition text-xs whitespace-nowrap">Paging vs Segmentation?</button>
                        <button onclick="quickAsk('Quiz me on multitasking')" class="px-3 py-1 rounded-full bg-white/10 hover:bg-white/20 transition text-xs whitespace-nowrap">Quiz me on multitasking</button>
                    </div>
                    <div class="flex gap-2">
                        <input type="text" id="chat-input" placeholder="Ask anything about your study materials..." 
                            class="flex-1 px-4 py-3 rounded-xl bg-white/10 border border-white/10 focus:outline-none focus:border-cyan-500/50 text-white placeholder-gray-500"
                            onkeypress="if(event.key==='Enter') sendMessage()">
                        <button onclick="sendMessage()" class="px-4 py-3 rounded-xl bg-gradient-to-r from-cyan-600 to-blue-600 hover:from-cyan-500 hover:to-blue-500 transition">
                            <i data-lucide="send" class="w-5 h-5"></i>
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Features Grid -->
    <section id="features" class="py-20 px-4 sm:px-6 lg:px-8 bg-white/5">
        <div class="max-w-7xl mx-auto">
            <div class="text-center mb-16">
                <h2 class="font-display text-4xl font-bold mb-4">Everything You Need to <span class="gradient-text">Ace Your Exams</span></h2>
                <p class="text-gray-400 max-w-2xl mx-auto">Powerful AI tools designed to transform how you learn, retain, and master any subject.</p>
            </div>

            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div class="glass rounded-2xl p-6 hover:bg-white/10 transition group">
                    <div class="w-12 h-12 rounded-xl bg-indigo-500/20 flex items-center justify-center mb-4 group-hover:scale-110 transition">
                        <i data-lucide="file-text" class="w-6 h-6 text-indigo-400"></i>
                    </div>
                    <h3 class="text-lg font-semibold mb-2">Smart Note Generation</h3>
                    <p class="text-sm text-gray-400">Upload any PDF, video, or audio and get structured, comprehensive notes instantly.</p>
                </div>

                <div class="glass rounded-2xl p-6 hover:bg-white/10 transition group">
                    <div class="w-12 h-12 rounded-xl bg-purple-500/20 flex items-center justify-center mb-4 group-hover:scale-110 transition">
                        <i data-lucide="layers" class="w-6 h-6 text-purple-400"></i>
                    </div>
                    <h3 class="text-lg font-semibold mb-2">AI Flashcards</h3>
                    <p class="text-sm text-gray-400">Automatic flashcard creation with spaced repetition to maximize retention.</p>
                </div>

                <div class="glass rounded-2xl p-6 hover:bg-white/10 transition group">
                    <div class="w-12 h-12 rounded-xl bg-pink-500/20 flex items-center justify-center mb-4 group-hover:scale-110 transition">
                        <i data-lucide="help-circle" class="w-6 h-6 text-pink-400"></i>
                    </div>
                    <h3 class="text-lg font-semibold mb-2">Practice Quizzes</h3>
                    <p class="text-sm text-gray-400">Unlimited quiz questions tailored to your materials with detailed explanations.</p>
                </div>

                <div class="glass rounded-2xl p-6 hover:bg-white/10 transition group">
                    <div class="w-12 h-12 rounded-xl bg-cyan-500/20 flex items-center justify-center mb-4 group-hover:scale-110 transition">
                        <i data-lucide="message-square" class="w-6 h-6 text-cyan-400"></i>
                    </div>
                    <h3 class="text-lg font-semibold mb-2">AI Tutor Chat</h3>
                    <p class="text-sm text-gray-400">Chat with Leo about your materials. Get explanations, examples, and clarifications.</p>
                </div>

                <div class="glass rounded-2xl p-6 hover:bg-white/10 transition group">
                    <div class="w-12 h-12 rounded-xl bg-yellow-500/20 flex items-center justify-center mb-4 group-hover:scale-110 transition">
                        <i data-lucide="mic" class="w-6 h-6 text-yellow-400"></i>
                    </div>
                    <h3 class="text-lg font-semibold mb-2">Lecture Recording</h3>
                    <p class="text-sm text-gray-400">Record live lectures and convert them to searchable notes and study guides.</p>
                </div>

                <div class="glass rounded-2xl p-6 hover:bg-white/10 transition group">
                    <div class="w-12 h-12 rounded-xl bg-green-500/20 flex items-center justify-center mb-4 group-hover:scale-110 transition">
                        <i data-lucide="users" class="w-6 h-6 text-green-400"></i>
                    </div>
                    <h3 class="text-lg font-semibold mb-2">Collaboration</h3>
                    <p class="text-sm text-gray-400">Share study sets with classmates. Study together in real-time with AI assistance.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="py-12 px-4 sm:px-6 lg:px-8 border-t border-white/10">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center gap-6">
            <div class="flex items-center gap-3">
                <div class="w-8 h-8 rounded-lg bg-gradient-to-br from-indigo-500 to-purple-600 flex items-center justify-center">
                    <i data-lucide="brain" class="w-5 h-5 text-white"></i>
                </div>
                <span class="font-display font-bold">Leo AI</span>
            </div>
            <p class="text-sm text-gray-500">© 2026 Leo AI. All rights reserved.</p>
            <div class="flex gap-6">
                <a href="#" class="text-gray-400 hover:text-white transition">Privacy</a>
                <a href="#" class="text-gray-400 hover:text-white transition">Terms</a>
                <a href="#" class="text-gray-400 hover:text-white transition">Support</a>
            </div>
        </div>
    </footer>

    <script>
        // Initialize Lucide icons
        lucide.createIcons();

        // Global state
        let currentTab = 'pdf';
        let currentStudyMode = 'notes';
        let currentCard = 0;
        let quizScore = 0;
        let currentQuestion = 0;
        let isRecording = false;
        let recordingInterval;
        let studyMaterials = {
            flashcards: [
                { q: "What is the primary role of an Operating System?", a: "To act as a 'playground monitor' managing hardware resources (CPU, memory, devices) and providing abstractions that make computers usable." },
                { q: "What is multitasking?", a: "The ability to run multiple programs seemingly simultaneously through rapid context switching and time-sharing." },
                { q: "What is virtual memory?", a: "An abstraction that gives each program its own memory space, isolating processes for security and allowing use of disk as extended RAM." },
                { q: "What is the Kernel?", a: "The core component of the OS with full hardware access, always resident in memory, managing system calls and resources." },
                { q: "What is paging?", a: "Dividing virtual memory into fixed-size blocks (pages) to allow non-contiguous physical memory allocation." },
                { q: "What is protected memory?", a: "Memory isolation ensuring processes cannot access each other's memory space, preventing crashes and security breaches." }
            ],
            quiz: [
                {
                    question: "Which component of the OS has full hardware access and remains resident in memory?",
                    options: ["Device Driver", "The Kernel", "File System", "Virtual Memory Manager"],
                    correct: 1,
                    explanation: "The Kernel is the core component with full hardware privileges, always kept in memory to handle system calls."
                },
                {
                    question: "What problem did batch processing originally solve?",
                    options: ["Slow internet speeds", "Computer idle time between jobs", "Too much memory usage", "Virus protection"],
                    correct: 1,
                    explanation: "Batch processing grouped programs together to run sequentially, reducing the idle time operators needed to prepare new jobs."
                },
                {
                    question: "What is 'thrashing' in memory management?",
                    options: ["Physical damage to RAM", "Excessive paging activity slowing down the system", "Deleting important files", "Overheating of the CPU"],
                    correct: 1,
                    explanation: "Thrashing occurs when the system spends more time moving pages between RAM and disk than executing programs."
                },
                {
                    question: "Which technique divides memory into fixed-size blocks?",
                    options: ["Segmentation", "Paging", "Fragmentation", "Caching"],
                    correct: 1,
                    explanation: "Paging divides memory into fixed-size blocks called pages, typically 4KB each."
                },
                {
                    question: "Why are device drivers necessary?",
                    options: ["To speed up the CPU", "To allow OS to communicate with diverse hardware", "To increase storage space", "To connect to the internet"],
                    correct: 1,
                    explanation: "Device drivers act as translators between the OS and hardware, abstracting device-specific details."
                }
            ]
        };

        // Tab switching
        function switchTab(tab) {
            currentTab = tab;
            
            // Update tab styles
            ['pdf', 'video', 'audio', 'text'].forEach(t => {
                const btn = document.getElementById(`tab-${t}`);
                if (t === tab) {
                    btn.classList.add('tab-active');
                    btn.classList.remove('bg-white/5', 'text-gray-400');
                } else {
                    btn.classList.remove('tab-active');
                    btn.classList.add('bg-white/5', 'text-gray-400');
                }
            });

            // Show/hide appropriate input areas
            document.getElementById('upload-area').classList.toggle('hidden', tab !== 'pdf');
            document.getElementById('url-input-area').classList.toggle('hidden', tab !== 'video');
            document.getElementById('recording-area').classList.toggle('hidden', tab !== 'audio');
            document.getElementById('text-input-area').classList.toggle('hidden', tab !== 'text');
        }

        // File handling
        function handleDragOver(e) {
            e.preventDefault();
            e.currentTarget.classList.add('border-indigo-500');
        }

        function handleDrop(e) {
            e.preventDefault();
            e.currentTarget.classList.remove('border-indigo-500');
            const files = e.dataTransfer.files;
            if (files.length > 0) processFile(files[0]);
        }

        function handleFileSelect(e) {
            const file = e.target.files[0];
            if (file) processFile(file);
        }

        function processFile(file) {
            showProcessing();
            
            // Simulate processing steps
            setTimeout(() => {
                document.getElementById('processing-step').textContent = "Analyzing document structure...";
            }, 1000);
            
            setTimeout(() => {
                document.getElementById('processing-step').textContent = "Extracting key concepts...";
            }, 2000);
            
            setTimeout(() => {
                document.getElementById('processing-step').textContent = "Generating study materials...";
            }, 3000);
            
            setTimeout(() => {
                showStudyDashboard();
            }, 4000);
        }

        function processURL() {
            const url = document.querySelector('#url-input-area input').value;
            if (!url) return alert('Please enter a URL');
            showProcessing();
            
            setTimeout(() => {
                document.getElementById('processing-step').textContent = "Transcribing video content...";
            }, 1500);
            
            setTimeout(() => {
                showStudyDashboard();
            }, 3500);
        }

        function processText() {
            const text = document.querySelector('#text-input-area textarea').value;
            if (!text.trim()) return alert('Please enter some text');
            showProcessing();
            
            setTimeout(() => {
                showStudyDashboard();
            }, 2000);
        }

        function showProcessing() {
            document.getElementById('processing').classList.remove('hidden');
            document.getElementById('upload-area').classList.add('hidden');
            document.getElementById('url-input-area').classList.add('hidden');
            document.getElementById('recording-area').classList.add('hidden');
            document.getElementById('text-input-area').classList.add('hidden');
        }

        function showStudyDashboard() {
            document.getElementById('upload').classList.add('hidden');
            document.getElementById('study').classList.remove('hidden');
            document.getElementById('processing').classList.add('hidden');
            
            // Update card total
            document.getElementById('card-total').textContent = studyMaterials.flashcards.length;
            
            // Scroll to study section
            document.getElementById('study').scrollIntoView({ behavior: 'smooth' });
        }

        function scrollToUpload() {
            document.getElementById('upload').scrollIntoView({ behavior: 'smooth' });
        }

        // Study Mode Switching
        function switchStudyMode(mode) {
            currentStudyMode = mode;
            
            // Update mode cards
            ['notes', 'flashcards', 'quiz', 'chat'].forEach(m => {
                const btn = document.getElementById(`mode-${m}`);
                if (m === mode) {
                    btn.classList.add('tab-active');
                    btn.classList.remove('bg-white/5');
                } else {
                    btn.classList.remove('tab-active');
                    btn.classList.add('bg-white/5');
                }
            });
            
            // Show/hide views
            ['notes', 'flashcards', 'quiz', 'chat'].forEach(m => {
                document.getElementById(`view-${m}`).classList.toggle('hidden', m !== mode);
            });
            
            lucide.createIcons();
        }

        // Flashcard functions
        function flipCard() {
            document.getElementById('flashcard').classList.toggle('flipped');
        }

        function updateCard() {
            const card = studyMaterials.flashcards[currentCard];
            document.getElementById('card-question').textContent = card.q;
            document.getElementById('card-answer').textContent = card.a;
            document.getElementById('card-current').textContent = currentCard + 1;
            
            // Reset flip
            document.getElementById('flashcard').classList.remove('flipped');
        }

        function nextCard() {
            if (currentCard < studyMaterials.flashcards.length - 1) {
                currentCard++;
                updateCard();
            }
        }

        function prevCard() {
            if (currentCard > 0) {
                currentCard--;
                updateCard();
            }
        }

        function markDifficult() {
            // Visual feedback
            const btn = event.currentTarget;
            btn.classList.add('bg-red-500/40');
            setTimeout(() => btn.classList.remove('bg-red-500/40'), 300);
            nextCard();
        }

        function markEasy() {
            // Update progress
            const progress = ((currentCard + 1) / studyMaterials.flashcards.length) * 100;
            document.getElementById('progress-bar').style.width = progress + '%';
            document.getElementById('progress-text').textContent = Math.round(progress) + '% Mastered';
            
            // Visual feedback
            const btn = event.currentTarget;
            btn.classList.add('bg-green-500/40');
            setTimeout(() => btn.classList.remove('bg-green-500/40'), 300);
            nextCard();
        }

        // Quiz functions
        function selectAnswer(index) {
            const question = studyMaterials.quiz[currentQuestion];
            const options = document.querySelectorAll('.quiz-option');
            
            options.forEach((opt, i) => {
                opt.disabled = true;
                if (i === question.correct) {
                    opt.classList.add('correct');
                } else if (i === index && i !== question.correct) {
                    opt.classList.add('wrong');
                }
            });
            
            const feedback = document.getElementById('quiz-feedback');
            const feedbackIcon = document.getElementById('feedback-icon');
            const feedbackTitle = document.getElementById('feedback-title');
            const feedbackText = document.getElementById('feedback-text');
            
            feedback.classList.remove('hidden');
            
            if (index === question.correct) {
                quizScore++;
                feedbackIcon.innerHTML = '<i data-lucide="check" class="w-4 h-4 text-green-400"></i>';
                feedbackIcon.className = 'w-6 h-6 rounded-full bg-green-500/20 flex items-center justify-center mt-0.5';
                feedbackTitle.textContent = 'Correct!';
                feedbackTitle.className = 'font-semibold mb-1 text-green-400';
                createConfetti();
            } else {
                feedbackIcon.innerHTML = '<i data-lucide="x" class="w-4 h-4 text-red-400"></i>';
                feedbackIcon.className = 'w-6 h-6 rounded-full bg-red-500/20 flex items-center justify-center mt-0.5';
                feedbackTitle.textContent = 'Incorrect';
                feedbackTitle.className = 'font-semibold mb-1 text-red-400';
            }
            
            feedbackText.textContent = question.explanation;
            document.getElementById('quiz-score').textContent = `${quizScore}/${currentQuestion + 1}`;
            
            document.getElementById('next-q-btn').classList.remove('hidden');
            lucide.createIcons();
        }

        function nextQuestion() {
            currentQuestion++;
            
            if (currentQuestion >= studyMaterials.quiz.length) {
                document.getElementById('quiz-container').classList.add('hidden');
                document.getElementById('quiz-complete').classList.remove('hidden');
                document.getElementById('final-score').textContent = `${quizScore}/${studyMaterials.quiz.length}`;
                if (quizScore === studyMaterials.quiz.length) createConfetti();
            } else {
                showQuestion();
            }
        }

        function showQuestion() {
            const q = studyMaterials.quiz[currentQuestion];
            document.getElementById('q-number').textContent = currentQuestion + 1;
            document.getElementById('q-text').textContent = q.question;
            
            const optionsContainer = document.getElementById('q-options');
            optionsContainer.innerHTML = '';
            
            q.options.forEach((opt, i) => {
                const btn = document.createElement('button');
                btn.className = 'quiz-option w-full p-4 rounded-xl glass text-left hover:bg-white/10 transition flex items-center gap-3';
                btn.onclick = () => selectAnswer(i);
                btn.innerHTML = `
                    <div class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center font-semibold text-sm">${String.fromCharCode(65 + i)}</div>
                    <span>${opt}</span>
                `;
                optionsContainer.appendChild(btn);
            });
            
            document.getElementById('quiz-feedback').classList.add('hidden');
            document.getElementById('next-q-btn').classList.add('hidden');
        }

        function restartQuiz() {
            currentQuestion = 0;
            quizScore = 0;
            document.getElementById('quiz-score').textContent = '0/0';
            document.getElementById('quiz-container').classList.remove('hidden');
            document.getElementById('quiz-complete').classList.add('hidden');
            showQuestion();
        }

        // Chat functions
        function sendMessage() {
            const input = document.getElementById('chat-input');
            const message = input.value.trim();
            if (!message) return;
            
            addMessage(message, 'user');
            input.value = '';
            
            // Simulate AI thinking
            setTimeout(() => {
                showTyping();
            }, 500);
            
            setTimeout(() => {
                removeTyping();
                const response = generateAIResponse(message);
                addMessage(response, 'ai');
            }, 2000);
        }

        function quickAsk(question) {
            document.getElementById('chat-input').value = question;
            sendMessage();
        }

        function addMessage(text, sender) {
            const container = document.getElementById('chat-messages');
            const div = document.createElement('div');
            div.className = 'chat-message flex gap-3 ' + (sender === 'user' ? 'flex-row-reverse' : '');
            
            if (sender === 'ai') {
                div.innerHTML = `
                    <div class="w-8 h-8 rounded-full bg-gradient-to-br from-cyan-500 to-blue-600 flex-shrink-0 flex items-center justify-center">
                        <i data-lucide="bot" class="w-4 h-4 text-white"></i>
                    </div>
                    <div class="glass rounded-2xl rounded-tl-none p-4 max-w-[80%]">
                        <p class="text-sm">${text}</p>
                    </div>
                `;
            } else {
                div.innerHTML = `
                    <div class="w-8 h-8 rounded-full bg-white/20 flex-shrink-0 flex items-center justify-center">
                        <i data-lucide="user" class="w-4 h-4 text-white"></i>
                    </div>
                    <div class="glass rounded-2xl rounded-tr-none p-4 max-w-[80%] bg-indigo-500/20">
                        <p class="text-sm">${text}</p>
                    </div>
                `;
            }
            
            container.appendChild(div);
            container.scrollTop = container.scrollHeight;
            lucide.createIcons();
        }

        function showTyping() {
            const container = document.getElementById('chat-messages');
            const div = document.createElement('div');
            div.id = 'typing-indicator';
            div.className = 'chat-message flex gap-3';
            div.innerHTML = `
                <div class="w-8 h-8 rounded-full bg-gradient-to-br from-cyan-500 to-blue-600 flex-shrink-0 flex items-center justify-center">
                    <i data-lucide="bot" class="w-4 h-4 text-white"></i>
                </div>
                <div class="glass rounded-2xl rounded-tl-none p-4">
                    <div class="flex gap-1">
                        <div class="w-2 h-2 rounded-full bg-cyan-400 typing-dot"></div>
                        <div class="w-2 h-2 rounded-full bg-cyan-400 typing-dot"></div>
                        <div class="w-2 h-2 rounded-full bg-cyan-400 typing-dot"></div>
                    </div>
                </div>
            `;
            container.appendChild(div);
            container.scrollTop = container.scrollHeight;
        }

        function removeTyping() {
            const indicator = document.getElementById('typing-indicator');
            if (indicator) indicator.remove();
        }

        function generateAIResponse(question) {
            const responses = {
                'virtual memory': "Virtual memory is a memory management technique that creates an abstraction of the available memory resources. It gives each process the illusion of having a large, contiguous address space, while physically the memory may be fragmented or even stored on disk. This allows for efficient memory isolation between processes!",
                'kernel': "The Kernel is the core component of the operating system. It's the bridge between applications and the actual hardware. It manages system calls, processes, memory, and device drivers. Think of it as the 'boss' that has full privileges to manage all computer resources.",
                'paging': "Paging solves the problem of external fragmentation by dividing memory into fixed-size blocks called 'pages' (typically 4KB). This allows non-contiguous physical memory allocation, meaning a program's memory can be scattered anywhere in RAM, not just one continuous block.",
                'multitasking': "Multitasking gives the illusion that multiple programs run simultaneously. In reality, the OS rapidly switches between processes (context switching), giving each a small time slice. This happens so fast that humans perceive it as parallel execution!",
                'default': "That's a great question about operating systems! Based on your study materials, this relates to how the OS manages resources efficiently. Would you like me to explain it with a specific example or analogy?"
            };
            
            const lower = question.toLowerCase();
            for (const key in responses) {
                if (lower.includes(key)) return responses[key];
            }
            return responses['default'];
        }

        function clearChat() {
            const container = document.getElementById('chat-messages');
            container.innerHTML = `
                <div class="chat-message flex gap-3">
                    <div class="w-8 h-8 rounded-full bg-gradient-to-br from-cyan-500 to-blue-600 flex-shrink-0 flex items-center justify-center">
                        <i data-lucide="bot" class="w-4 h-4 text-white"></i>
                    </div>
                    <div class="glass rounded-2xl rounded-tl-none p-4 max-w-[80%]">
                        <p class="text-sm">Chat cleared! I'm ready to help you study. What would you like to know about Operating Systems?</p>
                    </div>
                </div>
            `;
            lucide.createIcons();
        }

        // Recording simulation
        function toggleRecording() {
            const btn = document.getElementById('record-btn');
            const status = document.getElementById('recording-status');
            const timer = document.getElementById('recording-timer');
            
            if (!isRecording) {
                isRecording = true;
                btn.classList.add('scale-110');
                status.textContent = 'Recording...';
                timer.classList.remove('hidden');
                
                let seconds = 0;
                recordingInterval = setInterval(() => {
                    seconds++;
                    const mins = Math.floor(seconds / 60).toString().padStart(2, '0');
                    const secs = (seconds % 60).toString().padStart(2, '0');
                    timer.textContent = `${mins}:${secs}`;
                    
                    if (seconds > 3) {
                        clearInterval(recordingInterval);
                        showProcessing();
                        setTimeout(showStudyDashboard, 2000);
                    }
                }, 1000);
            } else {
                clearInterval(recordingInterval);
                isRecording = false;
                showProcessing();
                setTimeout(showStudyDashboard, 2000);
            }
        }

        // Utilities
        function createConfetti() {
            for (let i = 0; i < 50; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.background = ['#6366f1', '#a855f7', '#ec4899', '#06b6d4'][Math.floor(Math.random() * 4)];
                confetti.style.animationDelay = Math.random() * 2 + 's';
                document.body.appendChild(confetti);
                setTimeout(() => confetti.remove(), 3000);
            }
        }

        function exportContent(format) {
            alert(`Exporting as ${format.toUpperCase()}... (Demo feature)`);
        }

        function shareContent() {
            if (navigator.share) {
                navigator.share({
                    title: 'Leo AI Study Notes',
                    text: 'Check out my AI-generated study notes on Operating Systems!',
                    url: window.location.href
                });
            } else {
                alert('Link copied to clipboard! (Demo feature)');
            }
        }

        function toggleEdit() {
            const content = document.getElementById('notes-content');
            if (content.contentEditable === 'true') {
                content.contentEditable = 'false';
                content.classList.remove('border', 'border-indigo-500/50', 'p-4', 'rounded-xl');
            } else {
                content.contentEditable = 'true';
                content.classList.add('border', 'border-indigo-500/50', 'p-4', 'rounded-xl');
                content.focus();
            }
        }

        function toggleMobileMenu() {
            // Mobile menu toggle would go here
            alert('Mobile menu - Demo feature');
        }

        // Keyboard navigation for flashcards
        document.addEventListener('keydown', (e) => {
            if (currentStudyMode === 'flashcards') {
                if (e.key === 'ArrowRight') nextCard();
                if (e.key === 'ArrowLeft') prevCard();
                if (e.key === ' ' || e.key === 'Enter') flipCard();
            }
        });

        // Initialize
        window.onload = () => {
            lucide.createIcons();
        };
    </script>
</body>
</html>
