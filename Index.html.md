<!DOCTYPE html>  
<html lang="en" class="scroll-smooth">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>CoCo's Curated Rooms • Shop the Scene</title>  
    <script src="https://cdn.tailwindcss.com"></script>  
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">  
    <style>  
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Inter:wght@400;600&display=swap');  
        .logo { font-family: 'Playfair Display', serif; }  
        .hotspot {  
            position: absolute;  
            width: 42px;  
            height: 42px;  
            background: rgba(45, 212, 191, 0.15);  
            border: 3px solid #2dd4bf;  
            border-radius: 9999px;  
            display: flex;  
            align-items: center;  
            justify-content: center;  
            color: white;  
            font-weight: 700;  
            cursor: pointer;  
            box-shadow: 0 0 0 6px rgba(45, 212, 191, 0.3);  
            transition: all 0.3s;  
            animation: pulse 2s infinite;  
        }  
        .hotspot:hover { transform: scale(1.3); background: #14b8a6; }  
        @keyframes pulse {  
            0%, 100% { box-shadow: 0 0 0 6px rgba(45, 212, 191, 0.3); }  
            50% { box-shadow: 0 0 0 12px rgba(45, 212, 191, 0); }  
        }  
        .modal { animation: modalPop 0.3s ease-out; }  
        @keyframes modalPop { from { opacity: 0; transform: scale(0.95); } to { opacity: 1; transform: scale(1); } }  
    </style>  
</head>  
<body class="bg-zinc-50 text-zinc-900">  
  
    <!-- NAVBAR -->  
    <nav class="fixed top-0 w-full bg-white shadow-sm z-50">  
        <div class="max-w-7xl mx-auto px-6 py-5 flex justify-between items-center">  
            <div class="flex items-center gap-3">  
                <div class="w-8 h-8 bg-teal-500 rounded-xl flex items-center justify-center text-white font-bold text-xs">CC</div>  
                <span class="logo text-3xl tracking-tighter">CoCo's Curated Rooms</span>  
            </div>  
            <div class="hidden md:flex gap-8 text-sm font-medium">  
                <a href="#" onclick="showHome()" class="hover:text-teal-600 transition">Home</a>  
                <a href="#" onclick="showAllRooms()" class="hover:text-teal-600 transition">All Rooms</a>  
                <a href="#" class="hover:text-teal-600 transition">About</a>  
            </div>  
            <div class="text-xs bg-amber-100 text-amber-700 px-4 py-1.5 rounded-3xl flex items-center gap-2">  
                <i class="fa-solid fa-circle-check"></i>  
                Amazon Associate  
            </div>  
        </div>  
    </nav>  
  
    <!-- HOME / HERO -->  
    <div id="home-page">  
        <section class="pt-24 pb-16 bg-gradient-to-br from-zinc-900 to-zinc-800 text-white">  
            <div class="max-w-7xl mx-auto px-6 text-center">  
                <p class="uppercase tracking-[3px] text-teal-400 text-sm mb-4">Southfield, Michigan • Curated with ❤️</p>  
                <h1 class="text-6xl md:text-7xl font-bold logo leading-none mb-6">See it in the room.<br>Shop it on Amazon.</h1>  
                <p class="max-w-xl mx-auto text-xl text-zinc-300">Realistic room scenes. Click the items you love. Instant affiliate links.</p>  
                <button onclick="showAllRooms()" class="mt-10 px-10 py-5 bg-white text-zinc-900 font-semibold rounded-3xl text-lg hover:bg-teal-400 hover:text-white transition">Browse All Rooms</button>  
            </div>  
        </section>  
  
        <!-- FEATURED ROOMS GRID -->  
        <section class="max-w-7xl mx-auto px-6 py-16">  
            <h2 class="text-4xl font-semibold text-center mb-12">Featured Rooms</h2>  
            <div id="featured-grid" class="grid md:grid-cols-3 gap-8"></div>  
        </section>  
    </div>  
  
    <!-- INTERACTIVE ROOM VIEW -->  
    <div id="room-page" class="hidden">  
        <div class="max-w-7xl mx-auto px-6 pt-24 pb-12">  
            <button onclick="showHome()" class="flex items-center gap-2 text-teal-600 hover:text-teal-700 font-medium mb-8">  
                ← Back to All Rooms  
            </button>  
              
            <div class="flex justify-between items-end mb-6">  
                <div>  
                    <h1 id="room-title" class="text-5xl font-semibold"></h1>  
                    <p id="room-tagline" class="text-zinc-500 text-xl"></p>  
                </div>  
            </div>  
  
            <div id="room-container" class="relative rounded-3xl overflow-hidden shadow-2xl">  
                <img id="room-image" class="w-full h-auto" alt="Room">  
            </div>  
  
            <div class="mt-12 grid md:grid-cols-2 lg:grid-cols-3 gap-6" id="product-list"></div>  
        </div>  
    </div>  
  
    <!-- PRODUCT MODAL -->  
    <div id="product-modal" class="hidden fixed inset-0 bg-black/70 flex items-center justify-center z-[100]">  
        <div class="modal bg-white rounded-3xl max-w-lg w-full mx-4 overflow-hidden">  
            <div class="relative">  
                <img id="modal-image" class="w-full h-72 object-cover">  
                <button onclick="closeModal()" class="absolute top-4 right-4 bg-white rounded-full w-10 h-10 flex items-center justify-center shadow">  
                    ✕  
                </button>  
            </div>  
            <div class="p-8">  
                <div id="modal-name" class="text-3xl font-semibold mb-2"></div>  
                <div id="modal-price" class="text-2xl font-medium text-teal-600 mb-4"></div>  
                <div id="modal-desc" class="text-zinc-600 leading-relaxed mb-8"></div>  
                <a id="modal-link" target="_blank"   
                   class="block w-full text-center bg-gradient-to-r from-orange-500 to-amber-500 hover:from-orange-600 hover:to-amber-600 text-white font-bold py-5 rounded-3xl text-xl transition">  
                    Shop on Amazon <i class="fa-solid fa-arrow-up-right-from-square ml-2"></i>  
                </a>  
                <p class="text-center text-[10px] text-zinc-400 mt-6">As an Amazon Associate I earn from qualifying purchases</p>  
            </div>  
        </div>  
    </div>  
  
    <!-- FOOTER -->  
    <footer class="bg-zinc-900 text-zinc-400 py-12 text-center text-sm">  
        <div class="max-w-7xl mx-auto px-6">  
            <p>CoCo's Curated Rooms • Southfield, Michigan</p>  
            <p class="mt-4 text-xs max-w-md mx-auto">  
                As an Amazon Associate, I earn from qualifying purchases. Prices and availability are subject to change. All images are for demonstration purposes.  
            </p>  
            <p class="mt-8 text-xs">Built instantly with Grok • February 2026</p>  
        </div>  
    </footer>  
  
    <script>  
        const AFFILIATE_TAG = "coryvandestee-20";  
  
        const rooms = [  
            {  
                id: "living",  
                name: "Modern Living Room",  
                tagline: "Cozy evenings start here",  
                image: "https://picsum.photos/id/316/1200/800",  
                products: [  
                    { id:1, name:"Mjkone Velvet Sectional Sofa", price:"$1,299", asin:"B0DHZYKSDB", desc:"Ultra-soft 3-seater with chaise. Perfect for movie nights.", image:"https://picsum.photos/id/201/600/400", top:"48%", left:"22%" },  
                    { id:2, name:"Modern Marble Coffee Table", price:"$349", asin:"B0CTMHQL3Z", desc:"Elegant white marble top with gold legs.", image:"https://picsum.photos/id/251/600/400", top:"65%", left:"48%" },  
                    { id:3, name:"Ambimall Arc Floor Lamp", price:"$189", asin:"B0DJ7225F3", desc:"Warm LED light, adjustable height.", image:"https://picsum.photos/id/133/600/400", top:"35%", left:"68%" },  
                    { id:4, name:"Nakagishi Woven Area Rug", price:"$229", asin:"B0BRKNSBNS", desc:"Neutral tones, soft underfoot.", image:"https://picsum.photos/id/292/600/400", top:"78%", left:"35%" }  
                ]  
            },  
            {  
                id: "bedroom",  
                name: "Dream Bedroom",  
                tagline: "Your peaceful sanctuary",  
                image: "https://picsum.photos/id/251/1200/800",  
                products: [  
                    { id:1, name:"LIKIMIO King Bed Frame", price:"$899", asin:"B0B9XM2N74", desc:"Solid wood with upholstered headboard.", image:"https://picsum.photos/id/160/600/400", top:"42%", left:"35%" },  
                    { id:2, name:"Linen Duvet Set", price:"$129", asin:"B09W9Q6GR4", desc:"Breathable, stonewashed luxury.", image:"https://picsum.photos/id/175/600/400", top:"55%", left:"65%" }  
                ]  
            },  
            {  
                id: "office",  
                name: "Sleek Home Office",  
                tagline: "Work from home in style",  
                image: "https://picsum.photos/id/201/1200/800",  
                products: [  
                    { id:1, name:"SIHOO Ergonomic Office Chair", price:"$449", asin:"B07GNDDNMW", desc:"Mesh back, lumbar support.", image:"https://picsum.photos/id/180/600/400", top:"52%", left:"28%" },  
                    { id:2, name:"Floating Wall Desk", price:"$279", asin:"B0D8HY6K5D", desc:"Walnut finish, cable management.", image:"https://picsum.photos/id/290/600/400", top:"38%", left:"55%" }  
                ]  
            }  
        ];  
  
        function renderFeatured() {  
            const container = document.getElementById("featured-grid");  
            container.innerHTML = rooms.map(room => `  
                <div onclick="loadRoom('${room.id}')" class="group cursor-pointer">  
                    <div class="relative rounded-3xl overflow-hidden shadow-xl">  
                        <img src="${room.image}" class="w-full h-80 object-cover group-hover:scale-105 transition duration-500">  
                        <div class="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent"></div>  
                        <div class="absolute bottom-6 left-6 right-6">  
                            <div class="text-white text-3xl font-semibold">${room.name}</div>  
                            <div class="text-teal-300">${room.tagline}</div>  
                        </div>  
                    </div>  
                </div>  
            `).join('');  
        }  
  
        let currentRoom = null;  
  
        function loadRoom(id) {  
            currentRoom = rooms.find(r => r.id === id);  
            if (!currentRoom) return;  
  
            document.getElementById("home-page").classList.add("hidden");  
            document.getElementById("room-page").classList.remove("hidden");  
  
            document.getElementById("room-title").textContent = currentRoom.name;  
            document.getElementById("room-tagline").textContent = currentRoom.tagline;  
            document.getElementById("room-image").src = currentRoom.image;  
  
            const container = document.getElementById("room-container");  
            container.querySelectorAll('.hotspot').forEach(s => s.remove());  
  
            currentRoom.products.forEach(product => {  
                const spot = document.createElement("div");  
                spot.className = "hotspot text-sm";  
                spot.style.top = product.top;  
                spot.style.left = product.left;  
                spot.textContent = "🛍";  
                spot.onclick = (e) => { e.stopImmediatePropagation(); showProduct(product); };  
                container.appendChild(spot);  
            });  
  
            const list = document.getElementById("product-list");  
            list.innerHTML = currentRoom.products.map(p => `  
                <div onclick="showProductFromList(${[p.id](http://p.id)})" class="bg-white rounded-3xl overflow-hidden shadow hover:shadow-xl transition cursor-pointer">  
                    <img src="${p.image}" class="w-full h-48 object-cover">  
                    <div class="p-5">  
                        <div class="font-semibold">${p.name}</div>  
                        <div class="text-teal-600 text-xl font-medium">${p.price}</div>  
                    </div>  
                </div>  
            `).join('');  
        }  
  
        function showProduct(product) {  
            document.getElementById("modal-image").src = product.image;  
            document.getElementById("modal-name").textContent = product.name;  
            document.getElementById("modal-price").textContent = product.price;  
            document.getElementById("modal-desc").textContent = product.desc;  
            const link = `[https://www.amazon.com/dp/${product.asin}?tag=${AFFILIATE_TAG}`](https://www.amazon.com/dp/$%7Bproduct.asin%7D?tag=$%7BAFFILIATE_TAG%7D%60);  
            document.getElementById("modal-link").href = link;  
            const modal = document.getElementById("product-modal");  
            modal.classList.remove("hidden");  
            modal.classList.add("flex");  
        }  
  
        function showProductFromList(id) {  
            const product = currentRoom.products.find(p => p.id === id);  
            if (product) showProduct(product);  
        }  
  
        function closeModal() {  
            const modal = document.getElementById("product-modal");  
            modal.classList.add("hidden");  
            modal.classList.remove("flex");  
        }  
  
        function showHome() {  
            document.getElementById("room-page").classList.add("hidden");  
            document.getElementById("home-page").classList.remove("hidden");  
        }  
  
        function showAllRooms() {  
            showHome();  
        }  
  
        renderFeatured();  
        console.log("%c✅ CoCo's Curated Rooms LIVE with coryvandestee-20! All links track your commissions.", "color:#14b8a6; font-size:14px");  
    </script>  
</body>  
</html>  
