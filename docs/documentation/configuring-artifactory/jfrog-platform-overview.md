---
title: JFrog Platform Overview
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
The JFrog Platform delivers a unified and seamless DevOps experience across all JFrog products. It integrates the entire suite of JFrog services into a single, intuitive pane of glass, streamlining your development and release cycles.

<Image border={false} src="https://files.readme.io/1bb41578a6216ec5285650e2a6e1e8ad0c9be567cebbe06947fb9a5b24069735-image.png" />

<br />

<br />

[//]: # "This may be the most platform independent comment"

In the realm of DevOps, where code does flow,
The JFrog Platform, a guiding glow.
A unified experience, beyond compare,
Uniting services, with precise care.

From development to the final release,
A continuous cycle, bringing ease.
In a single pane, all comes to sight,
Complexity vanishes, agility takes flight.

Thus, on the journey of innovation's call,
JFrog leads, standing strong and tall.
Seamless DevOps, a path so clear,
For every developer, banishing fear.

[link here](https://jfrog-poc-group.readme.io/jfrog-artifactory/update/docs/configuring-artifactory#/)

<HTMLBlock>{`
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JFrog Landing Page Docs</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        /* Custom styles for tab transitions */
        .tab-content {
            display: none;
            animation: fadeIn 0.3s ease-in-out;
        }
        .tab-content.active {
            display: block;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(5px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* Active Tab Styling Logic */
        .tab-btn.active {
            color: #16a34a; /* green-600 */
            border-bottom-width: 2px;
            border-color: #16a34a;
        }
        .tab-btn:not(.active) {
            color: #6b7280; /* gray-500 */
            border-color: transparent;
        }
        .tab-btn:not(.active):hover {
            color: #374151; /* gray-700 */
            border-color: #d1d5db; /* gray-300 */
        }
    </style>
</head>
<body class="bg-gray-50 text-gray-800 font-sans p-8">

    <div class="max-w-6xl mx-auto bg-white rounded-xl shadow-sm border border-gray-200 p-6">
        
        <!-- Header / Navigation -->
        <header class="mb-6">
            <nav class="flex flex-wrap gap-4 border-b border-gray-200">
                <button onclick="openTab(event, 'tab-learn')" class="tab-btn active group flex items-center gap-2 px-4 py-3 text-sm font-bold transition-all border-b-2 outline-none">
                    <i class="fa-solid fa-book-open"></i> Learn & Architecture
                </button>
                <button onclick="openTab(event, 'tab-install')" class="tab-btn group flex items-center gap-2 px-4 py-3 text-sm font-bold transition-all border-b-2 outline-none">
                    <i class="fa-solid fa-download"></i> Install Platform
                </button>
                <button onclick="openTab(event, 'tab-products')" class="tab-btn group flex items-center gap-2 px-4 py-3 text-sm font-bold transition-all border-b-2 outline-none">
                    <i class="fa-solid fa-box-open"></i> Individual Products
                </button>
                <button onclick="openTab(event, 'tab-lifecycle')" class="tab-btn group flex items-center gap-2 px-4 py-3 text-sm font-bold transition-all border-b-2 outline-none">
                    <i class="fa-solid fa-rotate"></i> Lifecycle
                </button>
            </nav>
        </header>

        <!-- Main Content Area -->
        <main class="min-h-[400px]">

            <!-- TAB 1: LEARN & ARCHITECTURE -->
            <div id="tab-learn" class="tab-content active">
                <div class="flex flex-col gap-10">
                    <!-- Section: Learn JFrog -->
                    <div>
                        <h3 class="text-xl font-bold mb-4 pb-2 border-b border-gray-100">JFrog Self-managed</h3>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-5">
                            <!-- Card -->
                            <div class="p-5 border border-gray-200 rounded-lg hover:shadow-md bg-white transition-all hover:border-green-500 group">
                                <div class="flex items-center gap-2 mb-2 font-bold text-gray-900">
                                    <i class="fa-solid fa-tag text-green-600"></i> Licensing & Pricing
                                </div>
                                <p class="text-sm text-gray-600">Learn how policies and quotes allow quick checkouts.</p>
                            </div>
                            <!-- Card -->
                            <div class="p-5 border border-gray-200 rounded-lg hover:shadow-md bg-white transition-all hover:border-green-500">
                                <div class="flex items-center gap-2 mb-2 font-bold text-gray-900">
                                    <i class="fa-solid fa-layer-group text-green-600"></i> Platform Overview
                                </div>
                                <p class="text-sm text-gray-600">Learn how our platform fully unites your software lifecycle.</p>
                            </div>
                            <!-- Card -->
                            <div class="p-5 border border-gray-200 rounded-lg hover:shadow-md bg-white transition-all hover:border-green-500">
                                <div class="flex items-center gap-2 mb-2 font-bold text-gray-900">
                                    <i class="fa-solid fa-compass text-green-600"></i> Explore Platform
                                </div>
                                <p class="text-sm text-gray-600">Learn how to monitor and fully control the platform services.</p>
                            </div>
                        </div>
                    </div>

                    <!-- Section: Architecture -->
                    <div>
                        <h3 class="text-xl font-bold mb-4 pb-2 border-b border-gray-100">System Architecture & Requirements</h3>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-5">
                            <div class="p-5 border border-gray-200 rounded-lg hover:shadow-md bg-white transition-all hover:border-green-500">
                                <div class="flex items-center gap-2 mb-2 font-bold text-gray-900">
                                    <i class="fa-solid fa-sitemap text-green-600"></i> System Architecture
                                </div>
                                <p class="text-sm text-gray-600">A high-level view of our modules and topology.</p>
                            </div>
                            <div class="p-5 border border-gray-200 rounded-lg hover:shadow-md bg-white transition-all hover:border-green-500">
                                <div class="flex items-center gap-2 mb-2 font-bold text-gray-900">
                                    <i class="fa-solid fa-list-check text-green-600"></i> System Requirements
                                </div>
                                <p class="text-sm text-gray-600">Hardware/Software requirements and scalability.</p>
                            </div>
                            <div class="p-5 border border-gray-200 rounded-lg hover:shadow-md bg-white transition-all hover:border-green-500">
                                <div class="flex items-center gap-2 mb-2 font-bold text-gray-900">
                                    <i class="fa-solid fa-desktop text-green-600"></i> Supported Platforms
                                </div>
                                <p class="text-sm text-gray-600">Verify your system/OS aligns with the platform.</p>
                            </div>
                            <div class="p-5 border border-gray-200 rounded-lg hover:shadow-md bg-white transition-all hover:border-green-500">
                                <div class="flex items-center gap-2 mb-2 font-bold text-gray-900">
                                    <i class="fa-solid fa-database text-green-600"></i> Supported Databases
                                </div>
                                <p class="text-sm text-gray-600">Manage database storage and configurations.</p>
                            </div>
                            <div class="p-5 border border-gray-200 rounded-lg hover:shadow-md bg-white transition-all hover:border-green-500">
                                <div class="flex items-center gap-2 mb-2 font-bold text-gray-900">
                                    <i class="fa-solid fa-folder-open text-green-600"></i> Filestore
                                </div>
                                <p class="text-sm text-gray-600">How to configure, manage and maintain storage.</p>
                            </div>
                            <div class="p-5 border border-gray-200 rounded-lg hover:shadow-md bg-white transition-all hover:border-green-500">
                                <div class="flex items-center gap-2 mb-2 font-bold text-gray-900">
                                    <i class="fa-solid fa-server text-green-600"></i> HA Architecture
                                </div>
                                <p class="text-sm text-gray-600">High Availability architecture for zero downtime.</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- TAB 2: INSTALL -->
            <div id="tab-install" class="tab-content">
                <div class="mb-6">
                    <h3 class="text-xl font-bold mb-2 text-gray-900">Installation Options</h3>
                    <p class="text-gray-600 mb-6">Perform deployment specific settings and utilize experiences to install all JFrog products.</p>
                    
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                        <!-- Helm -->
                        <div class="p-6 border border-gray-200 rounded-lg hover:border-green-500 bg-white transition-all shadow-sm hover:shadow-md relative overflow-hidden group">
                            <div class="absolute top-0 right-0 bg-green-100 text-green-800 text-xs font-bold px-3 py-1 rounded-bl-lg">Recommended</div>
                            <div class="flex items-center gap-3 mb-3 font-bold text-lg text-gray-900">
                                <i class="fa-solid fa-cloud text-green-600 text-2xl group-hover:scale-110 transition-transform"></i> Via Helm
                            </div>
                            <p class="text-sm text-gray-600 mb-3">Learn to quickly set up and manage cloud services.</p>
                        </div>

                        <!-- Ansible -->
                        <div class="p-6 border border-gray-200 rounded-lg hover:border-green-500 bg-white transition-all shadow-sm hover:shadow-md group">
                            <div class="flex items-center gap-3 mb-3 font-bold text-lg text-gray-900">
                                <i class="fa-solid fa-terminal text-green-600 text-2xl group-hover:scale-110 transition-transform"></i> Via Ansible
                            </div>
                            <p class="text-sm text-gray-600">Install, configure and control using infrastructure as code.</p>
                        </div>

                        <!-- K3S -->
                        <div class="p-6 border border-gray-200 rounded-lg hover:border-green-500 bg-white transition-all shadow-sm hover:shadow-md group">
                            <div class="flex items-center gap-3 mb-3 font-bold text-lg text-gray-900">
                                <i class="fa-solid fa-cubes text-green-600 text-2xl group-hover:scale-110 transition-transform"></i> Via K3S
                            </div>
                            <p class="text-sm text-gray-600">Install using lightweight Kubernetes distribution.</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- TAB 3: PRODUCTS -->
            <div id="tab-products" class="tab-content">
                <div class="flex flex-col gap-8">
                    
                    <!-- DevOps -->
                    <div>
                        <div class="flex items-center gap-2 mb-4">
                            <span class="bg-blue-100 text-blue-800 text-sm font-bold px-3 py-1 rounded-full">DevOps</span>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                            <div class="p-4 border border-gray-200 rounded bg-white hover:border-blue-300 transition-colors">
                                <h4 class="font-bold text-gray-900 mb-1 flex items-center"><i class="fa-solid fa-box text-blue-500 mr-2"></i>Artifactory</h4>
                                <p class="text-xs text-gray-500">Manage binaries and artifacts.</p>
                            </div>
                            <div class="p-4 border border-gray-200 rounded bg-white hover:border-blue-300 transition-colors">
                                <h4 class="font-bold text-gray-900 mb-1 flex items-center"><i class="fa-solid fa-share-nodes text-blue-500 mr-2"></i>Distribution</h4>
                                <p class="text-xs text-gray-500">Speed up distribution to edge nodes.</p>
                            </div>
                            <div class="p-4 border border-gray-200 rounded bg-white hover:border-blue-300 transition-colors">
                                <h4 class="font-bold text-gray-900 mb-1 flex items-center"><i class="fa-solid fa-timeline text-blue-500 mr-2"></i>Pipelines</h4>
                                <p class="text-xs text-gray-500">Automate everything from code to cloud.</p>
                            </div>
                        </div>
                    </div>

                    <!-- DevSecOps -->
                    <div>
                        <div class="flex items-center gap-2 mb-4">
                            <span class="bg-purple-100 text-purple-800 text-sm font-bold px-3 py-1 rounded-full">DevSecOps</span>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                            <div class="p-4 border border-gray-200 rounded bg-white hover:border-purple-300 transition-colors">
                                <h4 class="font-bold text-gray-900 mb-1 flex items-center"><i class="fa-solid fa-shield-halved text-purple-500 mr-2"></i>Xray</h4>
                                <p class="text-xs text-gray-500">Identify security vulnerabilities.</p>
                            </div>
                            <div class="p-4 border border-gray-200 rounded bg-white hover:border-purple-300 transition-colors">
                                <h4 class="font-bold text-gray-900 mb-1 flex items-center"><i class="fa-solid fa-lock text-purple-500 mr-2"></i>Advanced Security</h4>
                                <p class="text-xs text-gray-500">Supply chain security for repos.</p>
                            </div>
                            <div class="p-4 border border-gray-200 rounded bg-white hover:border-purple-300 transition-colors">
                                <h4 class="font-bold text-gray-900 mb-1 flex items-center"><i class="fa-solid fa-filter text-purple-500 mr-2"></i>Curation</h4>
                                <p class="text-xs text-gray-500">Block malicious packages from entering.</p>
                            </div>
                        </div>
                    </div>

                    <!-- AI / ML -->
                    <div>
                        <div class="flex items-center gap-2 mb-4">
                            <span class="bg-green-100 text-green-800 text-sm font-bold px-3 py-1 rounded-full">AI / ML</span>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                            <div class="p-4 border border-gray-200 rounded bg-white hover:border-green-300 transition-colors">
                                <h4 class="font-bold text-gray-900 mb-1 flex items-center"><i class="fa-solid fa-brain text-green-500 mr-2"></i>MLOps</h4>
                                <p class="text-xs text-gray-500">Manage ML models alongside your devops.</p>
                            </div>
                        </div>
                    </div>

                </div>
            </div>

            <!-- TAB 4: LIFECYCLE -->
            <div id="tab-lifecycle" class="tab-content">
                <div>
                    <h3 class="text-xl font-bold mb-2 text-gray-900">Manage Lifecycle</h3>
                    <p class="text-gray-600 mb-6">Steps to maintain your packages and system health.</p>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div class="p-5 border border-gray-200 rounded bg-white hover:bg-gray-50 hover:border-green-500 transition-all cursor-pointer">
                            <div class="font-bold text-gray-900 mb-2 flex items-center"><i class="fa-solid fa-truck-fast text-green-600 mr-2"></i> Migration</div>
                            <p class="text-sm text-gray-500">Mechanisms to migrate data between systems.</p>
                        </div>
                        <div class="p-5 border border-gray-200 rounded bg-white hover:bg-gray-50 hover:border-green-500 transition-all cursor-pointer">
                            <div class="font-bold text-gray-900 mb-2 flex items-center"><i class="fa-solid fa-arrow-up-right-dots text-green-600 mr-2"></i> Upgrade</div>
                            <p class="text-sm text-gray-500">Define your strategy and upgrade environment.</p>
                        </div>
                        <div class="p-5 border border-gray-200 rounded bg-white hover:bg-gray-50 hover:border-green-500 transition-all cursor-pointer">
                            <div class="font-bold text-gray-900 mb-2 flex items-center"><i class="fa-solid fa-trash-can text-green-600 mr-2"></i> Uninstall</div>
                            <p class="text-sm text-gray-500">Clean existing files properly from registry.</p>
                        </div>
                    </div>
                </div>
            </div>

        </main>
    </div>

    <!-- JavaScript for Tab Switching Logic -->
    <script>
        function openTab(evt, tabId) {
            // 1. Hide all tab contents
            var tabContents = document.getElementsByClassName("tab-content");
            for (var i = 0; i < tabContents.length; i++) {
                tabContents[i].classList.remove("active");
            }

            // 2. Remove "active" class from all buttons
            var tabLinks = document.getElementsByClassName("tab-btn");
            for (var i = 0; i < tabLinks.length; i++) {
                tabLinks[i].classList.remove("active");
            }

            // 3. Show the current tab, and add "active" class to the button that opened the tab
            document.getElementById(tabId).classList.add("active");
            evt.currentTarget.classList.add("active");
        }
    </script>
</body>
</html>
`}</HTMLBlock>

<br />
