no right to chage the code!



<!DOCTYPE html><html lang="en"><head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>URL Shortener - Fast &amp; Free Link Shortening Tool</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    animation: {
                        'fade-in': 'fadeIn 0.6s ease-out',
                        'slide-up': 'slideUp 0.5s ease-out',
                        'slide-in': 'slideIn 0.4s ease-out',
                        'pulse-slow': 'pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                    },
                    keyframes: {
                        fadeIn: {
                            '0%': { opacity: '0' },
                            '100%': { opacity: '1' },
                        },
                        slideUp: {
                            '0%': { transform: 'translateY(20px)', opacity: '0' },
                            '100%': { transform: 'translateY(0)', opacity: '1' },
                        },
                        slideIn: {
                            '0%': { transform: 'translateX(-20px)', opacity: '0' },
                            '100%': { transform: 'translateX(0)', opacity: '1' },
                        },
                    }
                }
            }
        }
    </script>
    <style>
        body {
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 50%, #0f172a 100%);
            min-height: 100vh;
        }
        
        .glass {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .animated-bg {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            background-size: 200% 200%;
            animation: gradient 3s ease infinite;
        }
        
        @keyframes gradient {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        
        .glow {
            box-shadow: 0 0 20px rgba(102, 126, 234, 0.3);
        }
        
        .mesh-bg {
            background-image: 
                radial-gradient(at 40% 20%, rgba(102, 126, 234, 0.15) 0px, transparent 50%),
                radial-gradient(at 80% 0%, rgba(118, 75, 162, 0.15) 0px, transparent 50%),
                radial-gradient(at 0% 50%, rgba(99, 102, 241, 0.15) 0px, transparent 50%),
                radial-gradient(at 80% 100%, rgba(139, 92, 246, 0.15) 0px, transparent 50%),
                radial-gradient(at 0% 100%, rgba(236, 72, 153, 0.15) 0px, transparent 50%);
        }
    </style>
</head>
<body class="mesh-bg">
    <!-- Header -->
    <header class="text-center py-8 md:py-12 animate-fade-in">
        <h1 class="text-4xl md:text-6xl font-bold text-white mb-2 tracking-tight">
            <span class="bg-gradient-to-r from-purple-400 via-pink-400 to-indigo-400 bg-clip-text text-transparent">
                URL Shortener
            </span>
        </h1>
        <p class="text-gray-400 text-sm md:text-base">Fast, free, and beautiful link shortening by ExploitZ3r0</p>
    </header>

    <!-- Main Container -->
    <div class="container mx-auto px-4 max-w-6xl pb-16">
        <!-- Shortener Form -->
        <div class="glass rounded-2xl p-6 md:p-8 mb-8 animate-slide-up">
            <form id="urlShortenerForm" class="space-y-4">
                <div class="space-y-2">
                    <label for="originalUrl" class="block text-sm font-medium text-gray-300">Enter URL</label>
                    <input type="text" id="originalUrl" placeholder="https://example.com/very-long-url" required="" class="w-full px-4 py-3 bg-white/10 border border-white/20 rounded-lg text-white placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent transition-all duration-300"/>
                </div>
                
                <div class="space-y-2">
                    <label for="customAlias" class="block text-sm font-medium text-gray-300">Custom Alias (optional)</label>
                    <input type="text" id="customAlias" placeholder="my-custom-link" class="w-full px-4 py-3 bg-white/10 border border-white/20 rounded-lg text-white placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent transition-all duration-300"/>
                </div>
                
                <button type="submit" class="w-full py-3 px-6 animated-bg text-white font-semibold rounded-lg hover:scale-105 transform transition-all duration-300 glow">
                    Shorten URL
                </button>
            </form>
            
            <!-- Result Display -->
            <div id="resultContainer" class="mt-6 hidden">
                <div class="glass rounded-lg p-4 space-y-3">
                    <p class="text-sm text-gray-400">Shortened URL:</p>
                    <div class="flex flex-col sm:flex-row gap-3">
                        <a id="shortenedUrl" href="#" target="_blank" class="flex-1 text-purple-400 hover:text-purple-300 font-mono text-sm md:text-base break-all transition-colors duration-200"></a>
                        <button id="copyButton" class="px-6 py-2 bg-purple-600 hover:bg-purple-700 text-white rounded-lg transition-all duration-300 hover:scale-105 transform whitespace-nowrap">
                            Copy
                        </button>
                    </div>
                </div>
            </div>
            
            <!-- Error Display -->
            <div id="errorContainer" class="mt-4 hidden">
                <div class="bg-red-500/10 border border-red-500/20 rounded-lg p-4">
                    <p class="text-red-400 text-sm" id="errorMessage"></p>
                </div>
            </div>
        </div>

        <!-- URL History -->
        <div class="glass rounded-2xl p-6 md:p-8 animate-slide-up" style="animation-delay: 0.1s;">
            <div class="flex items-center justify-between mb-6">
                <h2 class="text-2xl font-bold text-white">Your Shortened URLs</h2>
                <button id="clearAllButton" class="px-4 py-2 bg-red-500/20 hover:bg-red-500/30 text-red-400 rounded-lg transition-all duration-300 text-sm font-medium">
                    Clear All
                </button>
            </div>
            
            <div id="historyContainer" class="space-y-3">
                <!-- History items will be inserted here -->
            </div>
            
            <div id="emptyState" class="text-center py-12 hidden">
                <svg class="mx-auto h-16 w-16 text-gray-600 mb-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.101m-.758-4.899a4 4 0 005.656 0l4-4a4 4 0 00-5.656-5.656l-1.1 1.1"></path>
                </svg>
                <p class="text-gray-500">No URLs shortened yet</p>
                <p class="text-gray-600 text-sm mt-2">Start by shortening your first URL above!</p>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="text-center py-8 text-gray-500 text-sm">
        <p class="mb-4">Created by <span class="text-purple-400 font-semibold">ExploitZ3r0</span></p>
    </footer>

    <!-- Floating Widget -->
    <div id="urlWidget" class="fixed bottom-6 right-6 z-50">
        <!-- Widget Panel (Hidden by default) -->
        <div id="widgetPanel" class="hidden mb-4 glass rounded-2xl p-6 w-80 shadow-2xl animate-slide-up">
            <div class="flex items-center justify-between mb-4">
                <h3 class="text-white font-bold">Quick Shorten</h3>
                <button onclick="toggleWidget()" class="text-gray-400 hover:text-white transition-colors">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                    </svg>
                </button>
            </div>
            
            <form id="widgetForm" class="space-y-3">
                <input type="text" id="widgetUrl" placeholder="Enter URL to shorten" required="" class="w-full px-3 py-2 bg-white/10 border border-white/20 rounded-lg text-white text-sm placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-purple-500 transition-all"/>
                <button type="submit" class="w-full py-2 px-4 animated-bg text-white font-semibold rounded-lg hover:scale-105 transform transition-all duration-300 text-sm">
                    Shorten
                </button>
            </form>
            
            <div id="widgetResult" class="mt-4 hidden">
                <div class="bg-white/10 rounded-lg p-3 space-y-2">
                    <p class="text-xs text-gray-400">Shortened:</p>
                    <div class="flex gap-2">
                        <a id="widgetShortUrl" href="#" target="_blank" class="flex-1 text-purple-400 font-mono text-xs break-all"></a>
                        <button onclick="copyWidgetUrl()" class="px-3 py-1 bg-purple-600 hover:bg-purple-700 text-white rounded text-xs transition-all">
                            Copy
                        </button>
                    </div>
                </div>
            </div>
            
            <div id="widgetError" class="mt-4 hidden">
                <div class="bg-red-500/10 border border-red-500/20 rounded-lg p-3">
                    <p class="text-red-400 text-xs" id="widgetErrorMsg"></p>
                </div>
            </div>
        </div>
        
        <!-- Widget Button -->
        <button id="widgetButton" onclick="toggleWidget()" class="w-16 h-16 rounded-full shadow-2xl hover:scale-110 transform transition-all duration-300 glow overflow-hidden bg-gray-900 border-2 border-red-500" title="Quick URL Shortener">
            <img src="https://cdn-ai.onspace.ai/onspace/project/uploads/GfmftsE7TKVnipUUBg4sNd/5963259a7_5a60156c-c371-4523-82a7-0845fe34cebb.jpeg" alt="URL Shortener Widget" class="w-full h-full object-cover"/>
        </button>
    </div>

    <script>
        // Load history from localStorage
        let urlHistory = JSON.parse(localStorage.getItem('urlHistory')) || [];

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            renderHistory();
        });

        // Form submission
        document.getElementById("urlShortenerForm").addEventListener("submit", function(event) {
            event.preventDefault();
            const originalUrl = document.getElementById("originalUrl").value;
            const customAlias = document.getElementById("customAlias").value;
            shortenUrl(originalUrl, customAlias);
        });

        // Shorten URL function
        function shortenUrl(originalUrl, customAlias) {
            // Show loading state
            const submitButton = document.querySelector('button[type="submit"]');
            const originalText = submitButton.textContent;
            submitButton.textContent = 'Shortening...';
            submitButton.disabled = true;

            let apiUrl = 'https://tinyurl.com/api-create.php?url=' + encodeURIComponent(originalUrl);
            if (customAlias) {
                apiUrl += '&alias=' + encodeURIComponent(customAlias);
            }

            fetch(apiUrl)
                .then(response => {
                    if (!response.ok) {
                        throw new Error('Alias not available or invalid URL');
                    }
                    return response.text();
                })
                .then(data => {
                    // Hide error, show result
                    document.getElementById("errorContainer").classList.add('hidden');
                    document.getElementById("resultContainer").classList.remove('hidden');
                    
                    const shortenedUrlElement = document.getElementById("shortenedUrl");
                    shortenedUrlElement.href = data;
                    shortenedUrlElement.textContent = data;
                    
                    // Save to history
                    saveToHistory(originalUrl, data);
                    
                    // Reset form
                    document.getElementById("urlShortenerForm").reset();
                    submitButton.textContent = originalText;
                    submitButton.disabled = false;
                })
                .catch(error => {
                    // Show error
                    document.getElementById("resultContainer").classList.add('hidden');
                    document.getElementById("errorContainer").classList.remove('hidden');
                    document.getElementById("errorMessage").textContent = error.message;
                    
                    submitButton.textContent = originalText;
                    submitButton.disabled = false;
                });
        }

        // Copy to clipboard
        document.getElementById("copyButton").addEventListener("click", function() {
            const url = document.getElementById("shortenedUrl").textContent;
            navigator.clipboard.writeText(url)
                .then(() => {
                    const button = document.getElementById("copyButton");
                    button.textContent = 'Copied!';
                    button.classList.add('bg-green-600', 'hover:bg-green-700');
                    button.classList.remove('bg-purple-600', 'hover:bg-purple-700');
                    
                    setTimeout(() => {
                        button.textContent = 'Copy';
                        button.classList.remove('bg-green-600', 'hover:bg-green-700');
                        button.classList.add('bg-purple-600', 'hover:bg-purple-700');
                    }, 2000);
                })
                .catch(err => console.error('Error copying: ', err));
        });

        // Save to history
        function saveToHistory(originalUrl, shortenedUrl) {
            const entry = {
                id: Date.now(),
                original: originalUrl,
                shortened: shortenedUrl,
                timestamp: new Date().toISOString()
            };
            
            urlHistory.unshift(entry);
            localStorage.setItem('urlHistory', JSON.stringify(urlHistory));
            renderHistory();
        }

        // Render history
        function renderHistory() {
            const container = document.getElementById("historyContainer");
            const emptyState = document.getElementById("emptyState");
            
            if (urlHistory.length === 0) {
                container.classList.add('hidden');
                emptyState.classList.remove('hidden');
                return;
            }
            
            container.classList.remove('hidden');
            emptyState.classList.add('hidden');
            
            container.innerHTML = urlHistory.map((entry, index) => `
                <div class="glass rounded-lg p-4 hover:bg-white/10 transition-all duration-300 animate-slide-in" style="animation-delay: ${index * 0.05}s;">
                    <div class="flex flex-col sm:flex-row sm:items-center gap-3">
                        <div class="flex-1 space-y-2 min-w-0">
                            <div class="flex items-start gap-2">
                                <span class="text-gray-500 text-xs mt-1 shrink-0">Original:</span>
                                <p class="text-gray-400 text-sm break-all">${entry.original}</p>
                            </div>
                            <div class="flex items-start gap-2">
                                <span class="text-gray-500 text-xs mt-1 shrink-0">Short:</span>
                                <a href="${entry.shortened}" target="_blank" class="text-purple-400 hover:text-purple-300 text-sm font-mono break-all transition-colors duration-200">${entry.shortened}</a>
                            </div>
                            <p class="text-gray-600 text-xs">${formatDate(entry.timestamp)}</p>
                        </div>
                        <div class="flex gap-2 sm:flex-col">
                            <button 
                                onclick="copyHistoryUrl('${entry.shortened}')"
                                class="px-4 py-2 bg-purple-600/20 hover:bg-purple-600/30 text-purple-400 rounded-lg transition-all duration-300 text-sm whitespace-nowrap"
                            >
                                Copy
                            </button>
                            <button 
                                onclick="deleteHistoryItem(${entry.id})"
                                class="px-4 py-2 bg-red-500/20 hover:bg-red-500/30 text-red-400 rounded-lg transition-all duration-300 text-sm whitespace-nowrap"
                            >
                                Delete
                            </button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        // Copy history URL
        function copyHistoryUrl(url) {
            navigator.clipboard.writeText(url)
                .then(() => {
                    // Could add a toast notification here
                    alert('URL copied to clipboard!');
                })
                .catch(err => console.error('Error copying: ', err));
        }

        // Delete history item
        function deleteHistoryItem(id) {
            urlHistory = urlHistory.filter(entry => entry.id !== id);
            localStorage.setItem('urlHistory', JSON.stringify(urlHistory));
            renderHistory();
        }

        // Clear all history
        document.getElementById("clearAllButton").addEventListener("click", function() {
            if (confirm('Are you sure you want to clear all history?')) {
                urlHistory = [];
                localStorage.setItem('urlHistory', JSON.stringify(urlHistory));
                renderHistory();
            }
        });

        // Format date
        function formatDate(timestamp) {
            const date = new Date(timestamp);
            const now = new Date();
            const diffMs = now - date;
            const diffMins = Math.floor(diffMs / 60000);
            const diffHours = Math.floor(diffMs / 3600000);
            const diffDays = Math.floor(diffMs / 86400000);
            
            if (diffMins < 1) return 'Just now';
            if (diffMins < 60) return `${diffMins} minute${diffMins > 1 ? 's' : ''} ago`;
            if (diffHours < 24) return `${diffHours} hour${diffHours > 1 ? 's' : ''} ago`;
            if (diffDays < 7) return `${diffDays} day${diffDays > 1 ? 's' : ''} ago`;
            
            return date.toLocaleDateString();
        }

        // ===== WIDGET FUNCTIONALITY =====
        
        // Toggle widget panel
        function toggleWidget() {
            const panel = document.getElementById('widgetPanel');
            const button = document.getElementById('widgetButton');
            
            if (panel.classList.contains('hidden')) {
                panel.classList.remove('hidden');
                button.classList.add('scale-95');
            } else {
                panel.classList.add('hidden');
                button.classList.remove('scale-95');
                // Reset widget form
                document.getElementById('widgetForm').reset();
                document.getElementById('widgetResult').classList.add('hidden');
                document.getElementById('widgetError').classList.add('hidden');
            }
        }

        // Widget form submission
        document.getElementById('widgetForm').addEventListener('submit', function(event) {
            event.preventDefault();
            const url = document.getElementById('widgetUrl').value;
            shortenWidgetUrl(url);
        });

        // Shorten URL for widget
        function shortenWidgetUrl(originalUrl) {
            const submitButton = document.querySelector('#widgetForm button[type="submit"]');
            const originalText = submitButton.textContent;
            submitButton.textContent = 'Shortening...';
            submitButton.disabled = true;

            const apiUrl = 'https://tinyurl.com/api-create.php?url=' + encodeURIComponent(originalUrl);

            fetch(apiUrl)
                .then(response => {
                    if (!response.ok) {
                        throw new Error('Invalid URL');
                    }
                    return response.text();
                })
                .then(data => {
                    document.getElementById('widgetError').classList.add('hidden');
                    document.getElementById('widgetResult').classList.remove('hidden');
                    
                    const shortUrlElement = document.getElementById('widgetShortUrl');
                    shortUrlElement.href = data;
                    shortUrlElement.textContent = data;
                    
                    // Save to main history
                    saveToHistory(originalUrl, data);
                    
                    // Reset form
                    document.getElementById('widgetForm').reset();
                    submitButton.textContent = originalText;
                    submitButton.disabled = false;
                })
                .catch(error => {
                    document.getElementById('widgetResult').classList.add('hidden');
                    document.getElementById('widgetError').classList.remove('hidden');
                    document.getElementById('widgetErrorMsg').textContent = error.message;
                    
                    submitButton.textContent = originalText;
                    submitButton.disabled = false;
                });
        }

        // Copy widget URL
        function copyWidgetUrl() {
            const url = document.getElementById('widgetShortUrl').textContent;
            navigator.clipboard.writeText(url)
                .then(() => {
                    const button = event.target;
                    button.textContent = 'Copied!';
                    button.classList.add('bg-green-600');
                    button.classList.remove('bg-purple-600');
                    
                    setTimeout(() => {
                        button.textContent = 'Copy';
                        button.classList.remove('bg-green-600');
                        button.classList.add('bg-purple-600');
                    }, 2000);
                })
                .catch(err => console.error('Error copying: ', err));
        }
    </script>


</body></html>
