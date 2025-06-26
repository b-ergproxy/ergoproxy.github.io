<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive 3D Resume</title>
    <script src="https://cdn.jsdelivr.net/npm/three@0.132.2/build/three.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #000;
            color: #fff;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        #canvas-container {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
        }

        .title {
            position: absolute;
            top: 20px;
            left: 0;
            width: 100%;
            text-align: center;
            font-size: 2.5rem;
            color: #fff;
            text-shadow: 0 0 10px #0ff, 0 0 20px #0ff;
            z-index: 2;
            letter-spacing: 3px;
        }

        .instructions {
            position: absolute;
            bottom: 30px;
            left: 0;
            width: 100%;
            text-align: center;
            color: #aaa;
            font-size: 1.1rem;
            z-index: 2;
        }

        .resume-section {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.9);
            width: 90%;
            max-width: 700px;
            height: 80vh;
            background: #e0ffff; /* Light cyan */
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 0 30px rgba(0, 200, 255, 0.7);
            z-index: 10;
            opacity: 0;
            visibility: hidden;
            transition: all 0.5s ease;
            overflow-y: auto;
            color: #333;
        }

        .resume-section.active {
            opacity: 1;
            visibility: visible;
            transform: translate(-50%, -50%) scale(1);
        }

        .close-btn {
            position: absolute;
            top: 15px;
            right: 15px;
            background: #ff5555;
            color: white;
            border: none;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            font-size: 18px;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: all 0.3s;
        }

        .close-btn:hover {
            background: #ff0000;
            transform: scale(1.1);
        }

        .section-title {
            text-align: center;
            margin-bottom: 25px;
            color: #0066cc;
            font-size: 2.2rem;
            border-bottom: 2px solid #00aaff;
            padding-bottom: 10px;
        }

        .content {
            margin-top: 20px;
        }

        .content h3 {
            color: #0088cc;
            margin-bottom: 10px;
            font-size: 1.5rem;
        }

        .content p {
            margin-bottom: 15px;
            line-height: 1.6;
        }

        .content ul {
            padding-left: 30px;
            margin-bottom: 20px;
        }

        .content li {
            margin-bottom: 8px;
        }

        .skill-bar {
            background: #c0c0c0;
            border-radius: 10px;
            margin: 10px 0 20px;
            height: 20px;
        }

        .skill-level {
            background: #00aaff;
            height: 100%;
            border-radius: 10px;
            text-align: right;
            padding-right: 10px;
            color: white;
            font-weight: bold;
        }

        @media (max-width: 768px) {
            .title {
                font-size: 1.8rem;
            }
            
            .instructions {
                font-size: 0.9rem;
            }
            
            .resume-section {
                padding: 20px;
                width: 95%;
            }
            
            .section-title {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>
    <div class="title">Interactive 3D Resume</div>
    <div id="canvas-container"></div>
    <div class="instructions">Click and drag to rotate the cube • Click a side to view details</div>

    <!-- Resume Sections -->
    <div id="about-section" class="resume-section">
        <button class="close-btn">×</button>
        <h2 class="section-title">About Me</h2>
        <div class="content">
            <p>Hello! I'm a passionate professional with expertise in web development and 3D graphics. I thrive on creating innovative solutions that blend creativity with technology.</p>
            <p>With over 5 years of experience in the industry, I've worked on diverse projects ranging from interactive websites to complex web applications.</p>
            <h3>Personal Philosophy</h3>
            <p>I believe in continuous learning and pushing the boundaries of what's possible. My approach combines technical excellence with user-centered design.</p>
        </div>
    </div>

    <div id="experience-section" class="resume-section">
        <button class="close-btn">×</button>
        <h2 class="section-title">Work Experience</h2>
        <div class="content">
            <h3>Senior Web Developer</h3>
            <p><strong>Tech Innovations Inc.</strong> | Jan 2020 - Present</p>
            <ul>
                <li>Developed interactive 3D web applications using Three.js</li>
                <li>Led a team of 5 developers in creating award-winning websites</li>
                <li>Implemented responsive designs for mobile and desktop</li>
                <li>Optimized website performance, reducing load time by 40%</li>
            </ul>

            <h3>Frontend Developer</h3>
            <p><strong>Digital Creations Co.</strong> | Mar 2017 - Dec 2019</p>
            <ul>
                <li>Created user interfaces for e-commerce platforms</li>
                <li>Integrated APIs with frontend applications</li>
                <li>Collaborated with UX designers to implement user-friendly interfaces</li>
                <li>Developed and maintained company's design system</li>
            </ul>
        </div>
    </div>

    <div id="skills-section" class="resume-section">
        <button class="close-btn">×</button>
        <h2 class="section-title">Skills & Expertise</h2>
        <div class="content">
            <h3>Technical Skills</h3>
            <p>JavaScript/TypeScript</p>
            <div class="skill-bar"><div class="skill-level" style="width: 95%">95%</div></div>
            
            <p>Three.js/WebGL</p>
            <div class="skill-bar"><div class="skill-level" style="width: 90%">90%</div></div>
            
            <p>React/Vue.js</p>
            <div class="skill-bar"><div class="skill-level" style="width: 85%">85%</div></div>
            
            <p>HTML5/CSS3</p>
            <div class="skill-bar"><div class="skill-level" style="width: 98%">98%</div></div>
            
            <p>Node.js/Express</p>
            <div class="skill-bar"><div class="skill-level" style="width: 80%">80%</div></div>
            
            <h3>Soft Skills</h3>
            <ul>
                <li>Problem Solving</li>
                <li>Team Leadership</li>
                <li>Project Management</li>
                <li>Creative Thinking</li>
                <li>Communication</li>
            </ul>
        </div>
    </div>

    <div id="education-section" class="resume-section">
        <button class="close-btn">×</button>
        <h2 class="section-title">Education</h2>
        <div class="content">
            <h3>Master of Computer Science</h3>
            <p><strong>University of Technology</strong> | 2015 - 2017</p>
            <p>Specialized in Computer Graphics and Human-Computer Interaction</p>
            <p>Graduated with honors</p>

            <h3>Bachelor of Web Development</h3>
            <p><strong>Digital Arts College</strong> | 2011 - 2015</p>
            <p>Focus on Frontend Technologies and Interactive Design</p>
            <p>Capstone project: Award-winning interactive web experience</p>
            
            <h3>Certifications</h3>
            <ul>
                <li>Advanced Three.js Developer Certification</li>
                <li>Google UX Design Professional Certificate</li>
                <li>AWS Certified Developer Associate</li>
                <li>Responsive Web Design Certification</li>
            </ul>
        </div>
    </div>

    <div id="projects-section" class="resume-section">
        <button class="close-btn">×</button>
        <h2 class="section-title">Projects</h2>
        <div class="content">
            <h3>Interactive 3D Portfolio</h3>
            <p>A fully interactive 3D portfolio website built with Three.js that allows users to explore projects in a virtual environment.</p>
            
            <h3>E-commerce Visualization Tool</h3>
            <p>Developed a web-based tool that allows customers to visualize products in 3D before purchasing. Increased conversion rates by 35%.</p>
            
            <h3>Virtual Art Gallery</h3>
            <p>Created a web-based virtual gallery showcasing digital art with real-time rendering and interactive elements.</p>
            
            <h3>Educational Web Game</h3>
            <p>Designed and developed an educational game for children that teaches programming concepts through interactive puzzles.</p>
        </div>
    </div>

    <div id="contact-section" class="resume-section">
        <button class="close-btn">×</button>
        <h2 class="section-title">Contact Me</h2>
        <div class="content">
            <h3>Get in Touch</h3>
            <p>I'm always open to discussing new projects, creative ideas, or opportunities to be part of your vision.</p>
            
            <div style="margin-top: 30px;">
                <p><strong>Email:</strong> contact@myresume.com</p>
                <p><strong>Phone:</strong> +1 (555) 123-4567</p>
                <p><strong>Location:</strong> Cebu City, Philippines</p>
            </div>
            
            <h3 style="margin-top: 30px;">Connect With Me</h3>
            <ul>
                <li>LinkedIn: linkedin.com/in/myprofile</li>
                <li>GitHub: github.com/myprofile</li>
                <li>Twitter: @myhandle</li>
                <li>Instagram: @myportfolio</li>
            </ul>
        </div>
    </div>

    <script>
        // Initialize Three.js
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
        
        // Set renderer size and add to container
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setClearColor(0x000000, 0); // Transparent background
        document.getElementById('canvas-container').appendChild(renderer.domElement);
        
        // Add lighting for the glowing effect
        const ambientLight = new THREE.AmbientLight(0x333333);
        scene.add(ambientLight);
        
        const pointLight = new THREE.PointLight(0xffffff, 1.5);
        pointLight.position.set(5, 5, 5);
        scene.add(pointLight);
        
        const pointLight2 = new THREE.PointLight(0xffffff, 1.5);
        pointLight2.position.set(-5, -5, -5);
        scene.add(pointLight2);
        
        // Create glowing white cube
        const cubeGeometry = new THREE.BoxGeometry(2.5, 2.5, 2.5);
        
        // Create a material with emissive property for glow effect
        const cubeMaterial = new THREE.MeshPhongMaterial({
            color: 0xffffff,
            emissive: 0xffffff,
            emissiveIntensity: 0.3,
            shininess: 100,
            specular: 0xffffff
        });
        
        const cube = new THREE.Mesh(cubeGeometry, cubeMaterial);
        scene.add(cube);
        
        // Position camera
        camera.position.z = 5;
        
        // Add rotation controls
        let isDragging = false;
        let previousMousePosition = {
            x: 0,
            y: 0
        };
        
        // Mouse event handlers
        document.addEventListener('mousedown', (e) => {
            isDragging = true;
        });
        
        document.addEventListener('mouseup', (e) => {
            isDragging = false;
        });
        
        document.addEventListener('mousemove', (e) => {
            const deltaMove = {
                x: e.offsetX - previousMousePosition.x,
                y: e.offsetY - previousMousePosition.y
            };
            
            if (isDragging) {
                const deltaRotationQuaternion = new THREE.Quaternion()
                    .setFromEuler(new THREE.Euler(
                        toRadians(deltaMove.y * 1),
                        toRadians(deltaMove.x * 1),
                        0,
                        'XYZ'
                    );
                
                cube.quaternion.multiplyQuaternions(deltaRotationQuaternion, cube.quaternion);
            }
            
            previousMousePosition = {
                x: e.offsetX,
                y: e.offsetY
            };
        });
        
        // Convert degrees to radians
        function toRadians(angle) {
            return angle * (Math.PI / 180);
        }
        
        // Handle window resize
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
        
        // Function to determine which face is front
        function getFrontFace() {
            // Create a raycaster from camera to cube center
            const raycaster = new THREE.Raycaster();
            raycaster.setFromCamera(new THREE.Vector2(0, 0), camera);
            
            // Get intersections
            const intersects = raycaster.intersectObject(cube);
            
            if (intersects.length > 0) {
                return intersects[0].faceIndex;
            }
            return -1;
        }
        
        // Animation and interaction loop
        let lastFace = -1;
        function animate() {
            requestAnimationFrame(animate);
            
            // Get current front face
            const currentFace = Math.floor(getFrontFace() / 2); // Each face has 2 triangles
            
            // Only trigger if face changes
            if (currentFace !== lastFace && currentFace !== -1) {
                lastFace = currentFace;
                
                // Show corresponding resume section
                const sections = [
                    'about-section',
                    'experience-section',
                    'skills-section',
                    'education-section',
                    'projects-section',
                    'contact-section'
                ];
                
                // Hide all sections first
                document.querySelectorAll('.resume-section').forEach(section => {
                    section.classList.remove('active');
                });
                
                // Show the current section
                document.getElementById(sections[currentFace]).classList.add('active');
            }
            
            // Add subtle automatic rotation
            if (!isDragging) {
                cube.rotation.x += 0.001;
                cube.rotation.y += 0.002;
            }
            
            renderer.render(scene, camera);
        }
        
        // Add event listeners for close buttons
        document.querySelectorAll('.close-btn').forEach(button => {
            button.addEventListener('click', () => {
                button.closest('.resume-section').classList.remove('active');
            });
        });
        
        // Start animation
        animate();
    </script>
</body>
</html>
