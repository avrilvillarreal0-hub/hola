<!DOCTYPE html>
<html lang="es" class="h-full bg-slate-100">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Atelier Design Studio - Diseña tu Prenda Personalizada</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Fabric.js CDN for interactive canvas elements -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fabric.js/5.3.1/fabric.min.js"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@500;700&family=Inter:wght@300;400;500;600;700&family=Playfair+Display:ital,wght@0,600;1,400&family=Pacifico&family=Oswald:wght@500;700&family=Montserrat:wght@400;700&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#fbf9f6',
                            100: '#f4ede4',
                            200: '#e6d8c5',
                            300: '#d5bca1',
                            400: '#c29c7d',
                            500: '#b0815e',
                            600: '#9d684e',
                            700: '#815141',
                            800: '#6a4237',
                            900: '#56382f',
                            gold: '#d4af37',
                            dark: '#1a1817'
                        }
                    },
                    fontFamily: {
                        serif: ['"Playfair Display"', 'serif'],
                        cinzel: ['"Cinzel"', 'serif'],
                        sans: ['Inter', 'sans-serif'],
                        pacifico: ['Pacifico', 'cursive'],
                        oswald: ['Oswald', 'sans-serif'],
                        montserrat: ['Montserrat', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <style>
        .gold-gradient {
            background: linear-gradient(135deg, #e5c158 0%, #c5a059 50%, #9e7a33 100%);
        }
        .canvas-container-outer {
            background-color: #ffffff;
            background-image: radial-gradient(#e2e8f0 1.2px, transparent 1.2px);
            background-size: 20px 20px;
        }
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        ::-webkit-scrollbar-thumb {
            background: #c5a059;
            border-radius: 4px;
        }
    </style>
</head>
<body class="h-full font-sans text-slate-800 flex flex-col min-h-screen selection:bg-brand-200">

    <!-- Top Header Navigation -->
    <header class="bg-brand-dark text-amber-50 shadow-md sticky top-0 z-40">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16">
                <!-- Brand Logo -->
                <div class="flex items-center space-x-3">
                    <div class="w-9 h-9 rounded-full gold-gradient flex items-center justify-center shadow">
                        <i class="fa-solid fa-wand-magic-sparkles text-slate-900 text-sm"></i>
                    </div>
                    <div>
                        <h1 class="font-cinzel text-lg font-bold tracking-wider text-amber-100">ATELIER <span class="text-brand-gold font-serif italic">Studio</span></h1>
                        <p class="text-[10px] text-stone-400 font-light tracking-widest uppercase -mt-1">Diseño & Confección a Medida</p>
                    </div>
                </div>

                <!-- Center Category Selector -->
                <div class="hidden md:flex items-center bg-stone-800/80 p-1 rounded-xl border border-stone-700">
                    <button onclick="setCategory('mujer')" id="cat-btn-mujer" class="cat-btn bg-brand-gold text-slate-950 px-4 py-1.5 rounded-lg text-xs font-bold transition flex items-center gap-1.5 shadow">
                        <i class="fa-solid fa-person-dress"></i> Mujer
                    </button>
                    <button onclick="setCategory('hombre')" id="cat-btn-hombre" class="cat-btn text-stone-300 hover:text-white px-4 py-1.5 rounded-lg text-xs font-semibold transition flex items-center gap-1.5">
                        <i class="fa-solid fa-person"></i> Hombre
                    </button>
                    <button onclick="setCategory('ninios')" id="cat-btn-ninios" class="cat-btn text-stone-300 hover:text-white px-4 py-1.5 rounded-lg text-xs font-semibold transition flex items-center gap-1.5">
                        <i class="fa-solid fa-child"></i> Niños / Niñas
                    </button>
                </div>

                <!-- Right Action Buttons -->
                <div class="flex items-center gap-2">
                    <button onclick="openPricingModal()" class="bg-stone-800 hover:bg-stone-700 text-stone-300 hover:text-white border border-stone-700 px-3 py-2 rounded-xl text-xs transition flex items-center gap-1.5">
                        <i class="fa-solid fa-gear text-brand-gold"></i> Configurar Tarifas
                    </button>
                    <button onclick="openOrderModal()" class="gold-gradient hover:opacity-90 text-slate-950 font-bold px-4 py-2 rounded-xl text-xs sm:text-sm shadow-lg transition flex items-center gap-2">
                        <i class="fa-solid fa-bag-shopping"></i> Solicitar Presupuesto
                    </button>
                </div>
            </div>
        </div>

        <!-- Mobile Category Selector Bar -->
        <div class="md:hidden bg-stone-900 border-t border-stone-800 px-3 py-2 flex justify-center gap-2">
            <button onclick="setCategory('mujer')" id="cat-btn-mujer-m" class="cat-btn-m bg-brand-gold text-slate-950 px-3 py-1 rounded-lg text-xs font-bold">Mujer</button>
            <button onclick="setCategory('hombre')" id="cat-btn-hombre-m" class="cat-btn-m text-stone-300 px-3 py-1 rounded-lg text-xs">Hombre</button>
            <button onclick="setCategory('ninios')" id="cat-btn-ninios-m" class="cat-btn-m text-stone-300 px-3 py-1 rounded-lg text-xs">Niños/as</button>
        </div>
    </header>

    <!-- Main Application Grid -->
    <main class="flex-1 max-w-7xl w-full mx-auto p-2 sm:p-4 lg:p-6 grid grid-cols-1 lg:grid-cols-12 gap-4 lg:gap-6 items-start">

        <!-- ================= LEFT PANEL: DESIGN TOOLS & CONTROLS ================= -->
        <aside class="lg:col-span-4 bg-white rounded-2xl shadow-sm border border-stone-200 overflow-hidden flex flex-col h-auto lg:h-[calc(100vh-6rem)] lg:sticky lg:top-20">
            
            <!-- Tool Navigation Tabs -->
            <div class="flex border-b border-stone-200 bg-stone-50 overflow-x-auto text-xs font-semibold text-slate-600">
                <button onclick="switchStudioTab('tab-garment')" id="tab-btn-garment" class="tool-tab active flex-1 py-3 px-3 text-center border-b-2 border-brand-gold text-slate-900 bg-white font-bold flex flex-col items-center gap-1 min-w-[70px]">
                    <i class="fa-solid fa-shirt text-brand-gold text-sm"></i> Prenda
                </button>
                <button onclick="switchStudioTab('tab-colors')" id="tab-btn-colors" class="tool-tab flex-1 py-3 px-3 text-center border-b-2 border-transparent hover:text-slate-900 flex flex-col items-center gap-1 min-w-[70px]">
                    <i class="fa-solid fa-palette text-sm"></i> Color/Patrón
                </button>
                <button onclick="switchStudioTab('tab-artwork')" id="tab-btn-artwork" class="tool-tab flex-1 py-3 px-3 text-center border-b-2 border-transparent hover:text-slate-900 flex flex-col items-center gap-1 min-w-[70px]">
                    <i class="fa-solid fa-icons text-sm"></i> Arte & Textos
                </button>
                <button onclick="switchStudioTab('tab-fabric')" id="tab-btn-fabric" class="tool-tab flex-1 py-3 px-3 text-center border-b-2 border-transparent hover:text-slate-900 flex flex-col items-center gap-1 min-w-[70px]">
                    <i class="fa-solid fa-scroll text-sm"></i> Telas
                </button>
                <button onclick="switchStudioTab('tab-size')" id="tab-btn-size" class="tool-tab flex-1 py-3 px-3 text-center border-b-2 border-transparent hover:text-slate-900 flex flex-col items-center gap-1 min-w-[70px]">
                    <i class="fa-solid fa-ruler-combined text-sm"></i> Medidas
                </button>
            </div>

            <!-- Tab Content Container -->
            <div class="p-4 overflow-y-auto flex-1 space-y-5">

                <!-- 1. GARMENT SELECTOR TAB -->
                <div id="tab-garment" class="tab-pane space-y-4">
                    <div>
                        <h3 class="text-sm font-bold text-slate-800 uppercase tracking-wider mb-1">Elija el Tipo de Prenda</h3>
                        <p class="text-xs text-slate-500">Seleccione el modelo base sobre el cual creará su diseño personalizado.</p>
                    </div>

                    <div id="garments-grid" class="grid grid-cols-2 gap-2.5">
                        <!-- Populated by JS -->
                    </div>
                </div>

                <!-- 2. COLOR & PATTERNS TAB -->
                <div id="tab-colors" class="tab-pane hidden space-y-5">
                    <div>
                        <label class="block text-xs font-bold text-slate-700 uppercase mb-2">1. Seleccionar Zona de la Prenda</label>
                        <div class="grid grid-cols-2 gap-2" id="zone-buttons-container">
                            <button onclick="selectZone('body')" id="zone-btn-body" class="zone-btn active bg-brand-dark text-white p-2 rounded-xl text-xs font-semibold flex items-center justify-center gap-2 shadow-sm">
                                <i class="fa-solid fa-shirt"></i> Cuerpo Principal
                            </button>
                            <button onclick="selectZone('sleeves')" id="zone-btn-sleeves" class="zone-btn bg-stone-100 hover:bg-stone-200 text-slate-700 p-2 rounded-xl text-xs font-semibold flex items-center justify-center gap-2">
                                <i class="fa-solid fa-hands"></i> Mangas
                            </button>
                            <button onclick="selectZone('collar')" id="zone-btn-collar" class="zone-btn bg-stone-100 hover:bg-stone-200 text-slate-700 p-2 rounded-xl text-xs font-semibold flex items-center justify-center gap-2">
                                <i class="fa-solid fa-circle-dot"></i> Cuello / Rib
                            </button>
                            <button onclick="selectZone('details')" id="zone-btn-details" class="zone-btn bg-stone-100 hover:bg-stone-200 text-slate-700 p-2 rounded-xl text-xs font-semibold flex items-center justify-center gap-2">
                                <i class="fa-solid fa-square-plus"></i> Detalles / Bolsillo
                            </button>
                        </div>
                    </div>

                    <hr class="border-stone-200">

                    <div>
                        <div class="flex justify-between items-center mb-2">
                            <label class="text-xs font-bold text-slate-700 uppercase">2. Color Sólido</label>
                            <input type="color" id="custom-color-picker" onchange="applySolidColor(this.value)" class="w-6 h-6 rounded cursor-pointer border-none">
                        </div>
                        <div class="grid grid-cols-7 gap-2" id="color-palette-grid">
                            <!-- Populated by JS -->
                        </div>
                    </div>

                    <hr class="border-stone-200">

                    <div>
                        <label class="block text-xs font-bold text-slate-700 uppercase mb-2">3. Patrones & Estampados de Fondo</label>
                        <div class="grid grid-cols-3 gap-2" id="patterns-grid">
                            <!-- Populated by JS -->
                        </div>
                        <button onclick="removeZonePattern()" class="w-full mt-2 text-xs text-rose-600 bg-rose-50 hover:bg-rose-100 py-1.5 rounded-lg font-medium transition">
                            <i class="fa-solid fa-xmark"></i> Quitar Patrón (Volver a Color Sólido)
                        </button>
                    </div>
                </div>

                <!-- 3. ARTWORK, TEXT, LOGO & STICKERS TAB -->
                <div id="tab-artwork" class="tab-pane hidden space-y-5">
                    <div class="bg-stone-50 p-3 rounded-xl border border-stone-200 space-y-3">
                        <label class="block text-xs font-bold text-slate-700 uppercase">
                            <i class="fa-solid fa-font text-brand-gold mr-1"></i> Agregar Texto o Frase
                        </label>
                        <input type="text" id="custom-text-input" placeholder="Escribe tu frase aquí..." class="w-full p-2 text-xs border border-stone-300 rounded-lg focus:ring-2 focus:ring-brand-gold outline-none">
                        
                        <div class="grid grid-cols-2 gap-2">
                            <div>
                                <label class="block text-[10px] text-slate-500 font-semibold mb-1">Tipografía</label>
                                <select id="text-font-family" class="w-full p-1.5 text-xs border border-stone-300 rounded-lg bg-white">
                                    <option value="Inter">Inter Clean</option>
                                    <option value="Playfair Display">Playfair Serif</option>
                                    <option value="Pacifico">Pacifico Script</option>
                                    <option value="Oswald">Oswald Bold</option>
                                    <option value="Montserrat">Montserrat</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-[10px] text-slate-500 font-semibold mb-1">Color de Texto</label>
                                <input type="color" id="text-color-picker" value="#ffffff" class="w-full h-8 rounded-lg cursor-pointer p-0 border border-stone-300">
                            </div>
                        </div>

                        <button onclick="addTextToCanvas()" class="w-full bg-slate-900 hover:bg-black text-white text-xs font-bold py-2 rounded-lg transition flex items-center justify-center gap-1 shadow">
                            <i class="fa-solid fa-plus text-xs"></i> Estampar Texto en Prenda
                        </button>
                    </div>

                    <div class="bg-stone-50 p-3 rounded-xl border border-stone-200 space-y-2">
                        <label class="block text-xs font-bold text-slate-700 uppercase">
                            <i class="fa-solid fa-cloud-arrow-up text-brand-gold mr-1"></i> Subir Tu Imagen o Logo
                        </label>
                        <p class="text-[11px] text-slate-500">Formato PNG transparente recomendado.</p>
                        <input type="file" id="image-upload-input" accept="image/*" onchange="handleImageUpload(event)" class="block w-full text-xs text-slate-500 file:mr-2 file:py-1.5 file:px-3 file:rounded-lg file:border-0 file:text-xs file:font-semibold file:bg-brand-gold file:text-slate-950 hover:file:opacity-90 cursor-pointer">
                    </div>

                    <div>
                        <label class="block text-xs font-bold text-slate-700 uppercase mb-2">
                            <i class="fa-solid fa-icons text-brand-gold mr-1"></i> Parches y Parches Bordados
                        </label>
                        <div class="grid grid-cols-4 gap-2" id="stickers-grid">
                            <!-- Populated by JS -->
                        </div>
                    </div>
                </div>

                <!-- 4. FABRIC & MATERIAL SELECTOR -->
                <div id="tab-fabric" class="tab-pane hidden space-y-4">
                    <div>
                        <h3 class="text-sm font-bold text-slate-800 uppercase tracking-wider mb-1">Elección de Tela y Composición</h3>
                        <p class="text-xs text-slate-500">Selecciona el textil ideal para la caída, comodidad y propósito de tu prenda.</p>
                    </div>

                    <div class="space-y-3" id="fabrics-list-container">
                        <!-- Populated by JS -->
                    </div>
                </div>

                <!-- 5. SIZE & CUSTOM MEASUREMENTS TAB -->
                <div id="tab-size" class="tab-pane hidden space-y-5">
                    <div>
                        <label class="block text-xs font-bold text-slate-700 uppercase mb-2">1. Talla Estándar</label>
                        <div class="flex flex-wrap gap-2" id="size-buttons-container">
                            <button onclick="selectStandardSize('XS')" class="size-btn border-2 border-stone-300 hover:border-brand-gold w-10 h-10 rounded-xl text-xs font-bold text-slate-700 flex items-center justify-center">XS</button>
                            <button onclick="selectStandardSize('S')" class="size-btn border-2 border-stone-300 hover:border-brand-gold w-10 h-10 rounded-xl text-xs font-bold text-slate-700 flex items-center justify-center">S</button>
                            <button onclick="selectStandardSize('M')" class="size-btn active border-2 border-brand-gold bg-brand-gold text-slate-950 w-10 h-10 rounded-xl text-xs font-bold flex items-center justify-center shadow-sm">M</button>
                            <button onclick="selectStandardSize('L')" class="size-btn border-2 border-stone-300 hover:border-brand-gold w-10 h-10 rounded-xl text-xs font-bold text-slate-700 flex items-center justify-center">L</button>
                            <button onclick="selectStandardSize('XL')" class="size-btn border-2 border-stone-300 hover:border-brand-gold w-10 h-10 rounded-xl text-xs font-bold text-slate-700 flex items-center justify-center">XL</button>
                            <button onclick="selectStandardSize('XXL')" class="size-btn border-2 border-stone-300 hover:border-brand-gold w-10 h-10 rounded-xl text-xs font-bold text-slate-700 flex items-center justify-center">XXL</button>
                        </div>
                    </div>

                    <hr class="border-stone-200">

                    <div class="space-y-3">
                        <div class="flex justify-between items-center">
                            <label class="text-xs font-bold text-slate-700 uppercase">2. O Ingresa tus Medidas Exactas (cm)</label>
                            <button onclick="toggleMeasurementGuide()" class="text-xs text-brand-700 hover:underline font-semibold flex items-center gap-1">
                                <i class="fa-solid fa-circle-info"></i> Guía Visual
                            </button>
                        </div>

                        <div class="grid grid-cols-2 gap-2 text-xs">
                            <div>
                                <label class="block text-[11px] text-slate-600 font-medium mb-1">Pecho / Busto</label>
                                <input type="number" id="meas-bust" placeholder="ej. 92" oninput="calculateFitAdvisor()" class="w-full p-2 border border-stone-300 rounded-lg">
                            </div>
                            <div>
                                <label class="block text-[11px] text-slate-600 font-medium mb-1">Cintura</label>
                                <input type="number" id="meas-waist" placeholder="ej. 74" oninput="calculateFitAdvisor()" class="w-full p-2 border border-stone-300 rounded-lg">
                            </div>
                            <div>
                                <label class="block text-[11px] text-slate-600 font-medium mb-1">Cadera</label>
                                <input type="number" id="meas-hip" placeholder="ej. 98" oninput="calculateFitAdvisor()" class="w-full p-2 border border-stone-300 rounded-lg">
                            </div>
                            <div>
                                <label class="block text-[11px] text-slate-600 font-medium mb-1">Largo Total</label>
                                <input type="number" id="meas-length" placeholder="ej. 65" oninput="calculateFitAdvisor()" class="w-full p-2 border border-stone-300 rounded-lg">
                            </div>
                        </div>
                    </div>

                    <div id="fit-advisor-box" class="bg-amber-50 border border-amber-200 p-3 rounded-xl flex items-start gap-3">
                        <div class="w-8 h-8 rounded-full gold-gradient flex items-center justify-center shrink-0 text-slate-950 mt-0.5">
                            <i class="fa-solid fa-wand-magic-sparkles text-xs"></i>
                        </div>
                        <div class="text-xs">
                            <span class="font-bold text-slate-800 block">Fit Advisor / Recomendación</span>
                            <p id="fit-advisor-text" class="text-slate-600 mt-0.5">Basado en la talla M estándar. Ingrese sus medidas arriba para ajustar a medida exacta.</p>
                        </div>
                    </div>
                </div>

            </div>

            <!-- Bottom Canvas Object Action Controls -->
            <div id="canvas-actions-bar" class="p-3 bg-stone-100 border-t border-stone-200 flex items-center justify-between text-xs">
                <span class="text-slate-500 font-medium">Controles de Capa:</span>
                <div class="flex items-center gap-1">
                    <button onclick="bringSelectedForward()" title="Traer Adelante" class="p-1.5 bg-white border border-stone-300 rounded hover:bg-stone-50"><i class="fa-solid fa-layer-group"></i></button>
                    <button onclick="deleteSelectedObject()" title="Eliminar Elemento" class="p-1.5 bg-rose-50 text-rose-600 border border-rose-200 rounded hover:bg-rose-100"><i class="fa-solid fa-trash-can"></i></button>
                    <button onclick="clearCanvasArt()" title="Limpiar Todo el Arte" class="p-1.5 bg-stone-200 text-slate-700 rounded hover:bg-stone-300"><i class="fa-solid fa-rotate-left"></i></button>
                </div>
            </div>
        </aside>

        <!-- ================= CENTER CANVAS: 2D VISUAL STUDIO ================= -->
        <section class="lg:col-span-8 space-y-4 flex flex-col">
            
            <!-- Canvas Header Toolbar -->
            <div class="bg-white p-3 rounded-2xl shadow-sm border border-stone-200 flex flex-wrap items-center justify-between gap-3">
                <div class="flex items-center bg-stone-100 p-1 rounded-xl">
                    <button onclick="setGarmentView('front')" id="view-btn-front" class="view-btn bg-slate-900 text-white px-4 py-1.5 rounded-lg text-xs font-bold transition shadow-sm flex items-center gap-1.5">
                        <i class="fa-solid fa-eye"></i> Vista Frontal
                    </button>
                    <button onclick="setGarmentView('back')" id="view-btn-back" class="view-btn text-slate-600 hover:text-slate-900 px-4 py-1.5 rounded-lg text-xs font-semibold transition flex items-center gap-1.5">
                        <i class="fa-solid fa-arrow-rotate-right"></i> Vista Trasera
                    </button>
                </div>

                <div class="text-center sm:text-left">
                    <span id="canvas-garment-title" class="font-serif font-bold text-slate-800 text-sm">Polera Urbana de Algodón</span>
                    <span id="canvas-fabric-badge" class="block text-[10px] text-brand-600 font-semibold">Tela: Algodón Premium</span>
                </div>

                <div class="flex items-center gap-2">
                    <button onclick="downloadDesignImage()" class="px-3 py-1.5 text-xs text-slate-700 bg-stone-100 hover:bg-stone-200 rounded-xl font-medium transition flex items-center gap-1 border border-stone-300">
                        <i class="fa-solid fa-download"></i> Guardar Imagen
                    </button>
                    <button onclick="saveDesignToLocal()" class="px-3 py-1.5 text-xs text-slate-800 bg-brand-100 hover:bg-brand-200 rounded-xl font-semibold transition flex items-center gap-1 border border-brand-300">
                        <i class="fa-solid fa-bookmark"></i> Guardar Borrador
                    </button>
                </div>
            </div>

            <!-- Canvas Display Stage -->
            <div class="bg-white p-4 sm:p-6 rounded-2xl shadow-sm border border-stone-200 flex flex-col items-center justify-center relative canvas-container-outer min-h-[520px]">
                <div class="relative shadow-2xl rounded-2xl overflow-hidden bg-white border border-stone-200" style="width: 380px; height: 480px;">
                    <div id="garment-svg-wrapper" class="absolute inset-0 w-full h-full flex items-center justify-center pointer-events-none p-4"></div>
                    <div class="absolute inset-0 w-full h-full">
                        <canvas id="apparel-canvas" width="380" height="480"></canvas>
                    </div>
                </div>
                <p class="text-[11px] text-slate-400 mt-3 italic flex items-center gap-1">
                    <i class="fa-solid fa-hand-pointer"></i> Haz clic y arrastra estampados o textos para posicionar, rotar o cambiar escala.
                </p>
            </div>

            <!-- Real-Time Quotation Breakdown Card -->
            <div class="bg-brand-dark text-stone-100 p-5 rounded-2xl shadow-xl border border-stone-800 grid grid-cols-1 md:grid-cols-12 gap-4 items-center">
                <div class="md:col-span-8 space-y-2">
                    <div class="flex items-center gap-2">
                        <span class="text-xs text-brand-gold font-bold uppercase tracking-widest">Presupuesto Estimado Automatizado</span>
                        <span id="summary-size-tag" class="bg-stone-800 text-stone-300 text-[10px] px-2 py-0.5 rounded-full font-bold">Talla: M</span>
                    </div>
                    
                    <div id="quotation-items-list" class="flex flex-wrap gap-x-4 gap-y-1 text-xs text-stone-300">
                        <!-- Populated by JS -->
                    </div>
                </div>

                <div class="md:col-span-4 flex flex-col items-end justify-center border-t md:border-t-0 md:border-l border-stone-800 pt-3 md:pt-0 md:pl-4">
                    <span class="text-[10px] text-stone-400 uppercase tracking-wider">Total Estimado (ARS)</span>
                    <span id="canvas-total-price" class="text-3xl font-serif font-bold text-brand-gold">$0</span>
                    <button onclick="openOrderModal()" class="w-full mt-2 gold-gradient text-slate-950 font-bold py-2 px-4 rounded-xl text-xs shadow hover:opacity-90 transition flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-paper-plane"></i> Solicitar Presupuesto al Taller
                    </button>
                </div>
            </div>

        </section>

    </main>

    <!-- ================= MODAL: PRICING CONFIGURATION (ADMIN / TAILOR) ================= -->
    <div id="pricing-modal" class="fixed inset-0 bg-slate-900/70 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4 overflow-y-auto">
        <div class="bg-white rounded-2xl shadow-2xl max-w-xl w-full my-8 overflow-hidden flex flex-col max-h-[90vh]">
            <div class="bg-brand-dark text-white p-5 flex justify-between items-center">
                <div>
                    <span class="text-xs text-brand-gold uppercase tracking-widest font-bold">Modo Sastre / Administrador</span>
                    <h3 class="text-xl font-serif font-bold text-amber-100">Configuración de Tarifas y Precios (ARS)</h3>
                </div>
                <button onclick="closePricingModal()" class="text-stone-400 hover:text-white text-xl"><i class="fa-solid fa-xmark"></i></button>
            </div>

            <div class="p-6 overflow-y-auto space-y-6 flex-1 text-xs">
                <p class="text-slate-500">Establezca los valores base en pesos argentinos. Los clientes calcularán su presupuesto en tiempo real según estos parámetros.</p>
                
                <!-- Garment Base Prices Section -->
                <div>
                    <h4 class="font-bold text-slate-800 uppercase tracking-wider mb-3 text-brand-700 border-b border-stone-200 pb-1">Precios Base por Prenda</h4>
                    <div id="pricing-garments-inputs" class="space-y-3">
                        <!-- Populated by JS -->
                    </div>
                </div>

                <!-- Fabric Addon Prices Section -->
                <div>
                    <h4 class="font-bold text-slate-800 uppercase tracking-wider mb-3 text-brand-700 border-b border-stone-200 pb-1">Adicionales por Tipo de Tela (ARS)</h4>
                    <div id="pricing-fabrics-inputs" class="space-y-3">
                        <!-- Populated by JS -->
                    </div>
                </div>

                <!-- Artwork Price Section -->
                <div>
                    <h4 class="font-bold text-slate-800 uppercase tracking-wider mb-3 text-brand-700 border-b border-stone-200 pb-1">Valor por Estampado / Texto / Parche (ARS)</h4>
                    <div class="flex items-center gap-3">
                        <label class="text-slate-700 font-medium">Precio por cada elemento añadido en el diseño:</label>
                        <input type="number" id="pricing-artwork-input" value="3500" class="w-32 p-2 border border-stone-300 rounded-lg text-right font-bold text-slate-800">
                    </div>
                </div>
            </div>

            <div class="p-4 bg-stone-50 border-t border-stone-200 flex justify-end gap-3">
                <button onclick="closePricingModal()" class="px-4 py-2 bg-stone-200 hover:bg-stone-300 text-slate-700 rounded-xl font-semibold">Cerrar</button>
                <button onclick="savePricingConfiguration()" class="gold-gradient text-slate-950 font-bold px-6 py-2 rounded-xl shadow">Guardar Tarifas</button>
            </div>
        </div>
    </div>

    <!-- ================= MODAL: VISUAL MEASUREMENT GUIDE ================= -->
    <div id="guide-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl shadow-2xl max-w-md w-full p-6 space-y-4">
            <div class="flex justify-between items-center border-b border-stone-200 pb-3">
                <h3 class="font-serif font-bold text-lg text-slate-800 flex items-center gap-2">
                    <i class="fa-solid fa-tape text-brand-gold"></i> Guía Visual de Toma de Medidas
                </h3>
                <button onclick="toggleMeasurementGuide()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            
            <div class="space-y-3 text-xs text-slate-600">
                <div class="p-3 bg-stone-50 rounded-xl border border-stone-200">
                    <strong class="text-slate-800 block text-sm">1. Busto / Pecho:</strong>
                    Pasa la cinta métrica por la parte más prominente del pecho, manteniendo la cinta horizontal.
                </div>
                <div class="p-3 bg-stone-50 rounded-xl border border-stone-200">
                    <strong class="text-slate-800 block text-sm">2. Cintura:</strong>
                    Mide alrededor de la parte más estrecha del torso (justo por encima del ombligo).
                </div>
                <div class="p-3 bg-stone-50 rounded-xl border border-stone-200">
                    <strong class="text-slate-800 block text-sm">3. Cadera:</strong>
                    Colócate de pie con los pies juntos y mide alrededor de la parte más ancha de las caderas.
                </div>
            </div>

            <button onclick="toggleMeasurementGuide()" class="w-full bg-slate-900 text-white font-bold py-2.5 rounded-xl text-xs">Entendido</button>
        </div>
    </div>

    <!-- ================= MODAL: ORDER & CONFECTION FORM ================= -->
    <div id="order-modal" class="fixed inset-0 bg-slate-900/70 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4 overflow-y-auto">
        <div class="bg-white rounded-2xl shadow-2xl max-w-2xl w-full my-8 overflow-hidden flex flex-col max-h-[90vh]">
            <div class="bg-brand-dark text-white p-5 flex justify-between items-center">
                <div>
                    <span class="text-xs text-brand-gold uppercase tracking-widest font-bold">Atelier & Confección</span>
                    <h3 class="text-xl font-serif font-bold text-amber-100">Solicitud de Presupuesto Personalizado</h3>
                </div>
                <button onclick="closeOrderModal()" class="text-stone-400 hover:text-white text-xl"><i class="fa-solid fa-xmark"></i></button>
            </div>

            <form onsubmit="submitCustomOrder(event)" class="p-6 overflow-y-auto space-y-5 flex-1">
                <div class="bg-brand-50 p-4 rounded-xl border border-brand-200 flex flex-wrap justify-between items-center gap-2">
                    <div>
                        <span id="order-summary-title" class="font-bold text-slate-800 text-sm">Polera Urbana Personalizada</span>
                        <p id="order-summary-details" class="text-xs text-slate-500">Categoría: Mujer | Talla: M | Tela: Algodón</p>
                    </div>
                    <div class="text-right">
                        <span class="text-[10px] text-slate-400 block uppercase">Presupuesto Estimado</span>
                        <span id="order-summary-price" class="text-xl font-bold text-brand-700">$0 ARS</span>
                    </div>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Nombre Completo *</label>
                        <input type="text" required placeholder="Ej. Sofía Martínez" class="w-full p-2.5 text-xs border border-stone-300 rounded-xl focus:ring-2 focus:ring-brand-gold outline-none">
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Correo Electrónico *</label>
                        <input type="email" required placeholder="tuemail@ejemplo.com" class="w-full p-2.5 text-xs border border-stone-300 rounded-xl focus:ring-2 focus:ring-brand-gold outline-none">
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Teléfono / WhatsApp *</label>
                        <input type="tel" required placeholder="+54 9 11 2345-6789" class="w-full p-2.5 text-xs border border-stone-300 rounded-xl focus:ring-2 focus:ring-brand-gold outline-none">
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Ciudad / Localidad</label>
                        <input type="text" placeholder="Ej. Rosario, Santa Fe" class="w-full p-2.5 text-xs border border-stone-300 rounded-xl focus:ring-2 focus:ring-brand-gold outline-none">
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Comentarios o Instrucciones Especiales para el Taller</label>
                    <textarea rows="3" placeholder="Ej. Deseo costuras reforzadas, entrega estimada para fecha particular..." class="w-full p-2.5 text-xs border border-stone-300 rounded-xl focus:ring-2 focus:ring-brand-gold outline-none"></textarea>
                </div>

                <div class="pt-3 border-t border-stone-200 flex justify-end gap-3">
                    <button type="button" onclick="closeOrderModal()" class="px-4 py-2.5 text-xs font-semibold text-slate-600 bg-stone-100 hover:bg-stone-200 rounded-xl">Cancelar</button>
                    <button type="submit" class="gold-gradient text-slate-950 font-bold px-6 py-2.5 rounded-xl text-xs shadow-lg hover:opacity-90 transition flex items-center gap-2">
                        <i class="fa-solid fa-paper-plane"></i> Enviar Solicitud al Taller
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Notification Toast Container -->
    <div id="toast-container" class="fixed top-20 right-4 z-50 space-y-2 pointer-events-none"></div>

    <!-- ================= JAVASCRIPT APPLICATION LOGIC ================= -->
    <script>
        /* -------------------------------------------------------------------------- */
        /*  DATA CATALOGS & USER-CONFIGURABLE PRICES                                  */
        /* -------------------------------------------------------------------------- */
        
        let garmentPrices = {
            mujer: { polera: 18500, vestido: 42000, hoodie: 38000, chaqueta: 58000, falda: 24000, pantalon: 35000 },
            hombre: { polera: 18500, camisa: 32000, hoodie: 38000, chaqueta: 60000, pantalon: 36000 },
            ninios: { polera: 14000, hoodie: 26000, vestido: 25000, pantalon: 22000 }
        };

        const GARMENT_CATALOG = {
            mujer: [
                { id: 'polera', name: 'Polera Urbana', desc: 'Corte femenino entallado' },
                { id: 'vestido', name: 'Vestido Casual', desc: 'Corte en A fluido' },
                { id: 'hoodie', name: 'Sudadera / Hoodie', desc: 'Capucha y bolsillo canguro' },
                { id: 'chaqueta', name: 'Chaqueta / Blazer', desc: 'Corte formal ajustado' },
                { id: 'falda', name: 'Falda Midi', desc: 'Pretina elastizada' },
                { id: 'pantalon', name: 'Pantalón Tailored', desc: 'Tiro alto' }
            ],
            hombre: [
                { id: 'polera', name: 'Polera Classic Fit', desc: 'Algodón pesado' },
                { id: 'camisa', name: 'Camisa Vestir/Casual', desc: 'Cuello estructurado' },
                { id: 'hoodie', name: 'Hoodie Oversize', desc: 'Bolsillo frontal' },
                { id: 'chaqueta', name: 'Chaqueta Biker/Denim', desc: 'Cierres metálicos' },
                { id: 'pantalon', name: 'Pantalón Chino', desc: 'Corte recto confort' }
            ],
            ninios: [
                { id: 'polera', name: 'Polera Infantil', desc: 'Súper suave e hipoalergénica' },
                { id: 'hoodie', name: 'Sudadera Niños/as', desc: 'Interior afelpado' },
                { id: 'vestido', name: 'Vestidito Infantil', desc: 'Con vuelo comodo' },
                { id: 'pantalon', name: 'Pantalón Jogger Kids', desc: 'Cintura ajustable' }
            ]
        };

        let fabricPrices = {
            algodon: 0,
            lino: 6500,
            seda: 9800,
            denim: 8000,
            lana: 7200
        };

        const FABRIC_CATALOG = [
            { id: 'algodon', name: 'Algodón Premium Comprimido', comp: '100% Algodón', desc: 'Suave, respirable y resistente.' },
            { id: 'lino', name: 'Lino Orgánico', comp: '100% Lino Natural', desc: 'Fresco, textura elegante y caída ligera.' },
            { id: 'seda', name: 'Seda Crepe / Satén', comp: 'Seda Sintética Deluxe', desc: 'Brillo sutil, fluidez extrema.' },
            { id: 'denim', name: 'Mezclilla / Denim 12oz', comp: '98% Algodón, 2% Elastano', desc: 'Resistente, estructurado con elasticidad.' },
            { id: 'lana', name: 'Lana / Tejido Térmico', comp: 'Mezcla Lana & Acrílico', desc: 'Cálido, ideal para invierno.' }
        ];

        let artworkUnitPrice = 3500;

        const PALETTE_COLORS = [
            '#ffffff', '#1a1817', '#9d684e', '#c5a059', '#dc2626', 
            '#2563eb', '#16a34a', '#ca8a04', '#9333ea', '#db2777', 
            '#475569', '#0d9488', '#ea580c', '#57534e'
        ];

        const PATTERNS_CATALOG = [
            { id: 'rayas', name: 'Rayas', svg: `<pattern id="p-rayas" width="20" height="20" patternTransform="rotate(45 0 0)" patternUnits="userSpaceOnUse"><line x1="0" y1="0" x2="0" y2="20" stroke="#000000" stroke-width="6" opacity="0.15"/></pattern>` },
            { id: 'lunares', name: 'Lunares', svg: `<pattern id="p-lunares" width="20" height="20" patternUnits="userSpaceOnUse"><circle cx="10" cy="10" r="4" fill="#000000" opacity="0.18"/></pattern>` },
            { id: 'cuadros', name: 'Cuadros Vichy', svg: `<pattern id="p-cuadros" width="20" height="20" patternUnits="userSpaceOnUse"><rect width="10" height="10" fill="#000000" opacity="0.15"/><rect x="10" y="10" width="10" height="10" fill="#000000" opacity="0.15"/></pattern>` },
            { id: 'flores', name: 'Floral Mini', svg: `<pattern id="p-flores" width="25" height="25" patternUnits="userSpaceOnUse"><circle cx="12" cy="12" r="3" fill="#e11d48" opacity="0.4"/><circle cx="12" cy="8" r="2" fill="#f43f5e" opacity="0.3"/><circle cx="16" cy="12" r="2" fill="#f43f5e" opacity="0.3"/></pattern>` }
        ];

        const STICKERS_CATALOG = [
            { name: 'Flor Rosa', icon: 'fa-flower-tulip', svg: `<svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24" fill="#e11d48"><path d="M12 2C8 2 5 6 5 10c0 4 3 7 7 10 4-3 7-6 7-10 0-4-3-8-7-8z"/></svg>` },
            { name: 'Estrella Gold', icon: 'fa-star', svg: `<svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24" fill="#d4af37"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>` },
            { name: 'Rayo Retro', icon: 'fa-bolt', svg: `<svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24" fill="#eab308"><path d="M11 15H6l7-14v8h5l-7 14v-8z"/></svg>` },
            { name: 'Corazón', icon: 'fa-heart', svg: `<svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" viewBox="0 0 24 24" fill="#dc2626"><path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg>` }
        ];

        /* -------------------------------------------------------------------------- */
        /*  STATE MANAGEMENT                                                          */
        /* -------------------------------------------------------------------------- */
        let state = {
            category: 'mujer',
            garment: 'polera',
            view: 'front',
            selectedZone: 'body',
            colors: { body: '#ffffff', sleeves: '#ffffff', collar: '#1a1817', details: '#ffffff' },
            patterns: { body: null, sleeves: null, collar: null, details: null },
            fabric: FABRIC_CATALOG[0],
            selectedSize: 'M',
            customMeasurements: { bust: '', waist: '', hip: '', length: '' }
        };

        let fabricCanvas;

        /* -------------------------------------------------------------------------- */
        /*  INITIALIZATION                                                            */
        /* -------------------------------------------------------------------------- */
        window.onload = function() {
            initFabricCanvas();
            renderGarmentsGrid();
            renderColorPalette();
            renderPatternsGrid();
            renderStickersGrid();
            renderFabricsList();
            updateGarmentVisual();
            updateQuotation();
        };

        function initFabricCanvas() {
            fabricCanvas = new fabric.Canvas('apparel-canvas', { selection: true });
            fabricCanvas.on('object:added', updateQuotation);
            fabricCanvas.on('object:removed', updateQuotation);
        }

        function formatARS(num) {
            return '$ ' + num.toLocaleString('es-AR');
        }

        /* -------------------------------------------------------------------------- */
        /*  UI RENDERERS & TAB SWITCHING                                              */
        /* -------------------------------------------------------------------------- */
        function setCategory(cat) {
            state.category = cat;
            document.querySelectorAll('.cat-btn, .cat-btn-m').forEach(btn => {
                btn.classList.remove('bg-brand-gold', 'text-slate-950', 'font-bold');
                btn.classList.add('text-stone-300');
            });
            const activeBtn = document.getElementById(`cat-btn-${cat}`);
            if (activeBtn) {
                activeBtn.classList.add('bg-brand-gold', 'text-slate-950', 'font-bold');
                activeBtn.classList.remove('text-stone-300');
            }

            const catList = GARMENT_CATALOG[cat];
            if (catList && catList.length > 0) {
                state.garment = catList[0].id;
            }
            renderGarmentsGrid();
            updateGarmentVisual();
            updateQuotation();
        }

        function switchStudioTab(tabId) {
            document.querySelectorAll('.tab-pane').forEach(el => el.classList.add('hidden'));
            document.getElementById(tabId).classList.remove('hidden');

            document.querySelectorAll('.tool-tab').forEach(btn => {
                btn.classList.remove('border-brand-gold', 'text-slate-900', 'bg-white', 'font-bold');
                btn.classList.add('border-transparent');
            });

            const activeTabBtn = document.getElementById(`tab-btn-${tabId.replace('tab-', '')}`);
            if (activeTabBtn) {
                activeTabBtn.classList.add('border-brand-gold', 'text-slate-900', 'bg-white', 'font-bold');
                activeTabBtn.classList.remove('border-transparent');
            }
        }

        function renderGarmentsGrid() {
            const container = document.getElementById('garments-grid');
            container.innerHTML = '';
            const list = GARMENT_CATALOG[state.category] || [];
            
            list.forEach(g => {
                const isSelected = state.garment === g.id;
                const price = (garmentPrices[state.category] && garmentPrices[state.category][g.id]) || 15000;
                
                const card = document.createElement('button');
                card.onclick = () => {
                    state.garment = g.id;
                    renderGarmentsGrid();
                    updateGarmentVisual();
                    updateQuotation();
                };
                card.className = `p-3 rounded-xl border-2 text-left transition flex flex-col justify-between ${
                    isSelected ? 'border-brand-gold bg-brand-50 shadow-sm' : 'border-stone-200 bg-white hover:border-stone-300'
                }`;

                card.innerHTML = `
                    <div>
                        <div class="flex justify-between items-center mb-1">
                            <span class="font-bold text-xs text-slate-800">${g.name}</span>
                            ${isSelected ? '<i class="fa-solid fa-circle-check text-brand-gold text-xs"></i>' : ''}
                        </div>
                        <p class="text-[10px] text-slate-500 line-clamp-2">${g.desc}</p>
                    </div>
                    <span class="text-xs font-bold text-brand-700 mt-2 block">${formatARS(price)}</span>
                `;
                container.appendChild(card);
            });
        }

        function renderColorPalette() {
            const grid = document.getElementById('color-palette-grid');
            grid.innerHTML = '';
            PALETTE_COLORS.forEach(hex => {
                const btn = document.createElement('button');
                btn.onclick = () => applySolidColor(hex);
                btn.className = 'w-7 h-7 rounded-lg border border-stone-300 shadow-sm transition hover:scale-110';
                btn.style.backgroundColor = hex;
                grid.appendChild(btn);
            });
        }

        function renderPatternsGrid() {
            const grid = document.getElementById('patterns-grid');
            grid.innerHTML = '';
            PATTERNS_CATALOG.forEach(p => {
                const btn = document.createElement('button');
                btn.onclick = () => applyPattern(p.id);
                btn.className = 'p-2 border border-stone-200 bg-stone-50 hover:bg-stone-100 rounded-xl text-center text-xs font-medium';
                btn.innerHTML = `<span class="block text-[10px] text-slate-700 font-bold">${p.name}</span>`;
                grid.appendChild(btn);
            });
        }

        function renderStickersGrid() {
            const grid = document.getElementById('stickers-grid');
            grid.innerHTML = '';
            STICKERS_CATALOG.forEach(s => {
                const btn = document.createElement('button');
                btn.onclick = () => addStickerToCanvas(s.svg);
                btn.className = 'p-2 bg-stone-50 hover:bg-stone-100 border border-stone-200 rounded-xl flex items-center justify-center text-slate-700 hover:text-brand-gold transition';
                btn.title = s.name;
                btn.innerHTML = `<i class="fa-solid ${s.icon} text-lg"></i>`;
                grid.appendChild(btn);
            });
        }

        function renderFabricsList() {
            const container = document.getElementById('fabrics-list-container');
            container.innerHTML = '';
            FABRIC_CATALOG.forEach(f => {
                const isSelected = state.fabric.id === f.id;
                const addPrice = fabricPrices[f.id] || 0;
                
                const card = document.createElement('div');
                card.onclick = () => {
                    state.fabric = f;
                    renderFabricsList();
                    updateGarmentVisual();
                    updateQuotation();
                };
                card.className = `p-3 rounded-xl border-2 cursor-pointer transition ${
                    isSelected ? 'border-brand-gold bg-brand-50' : 'border-stone-200 hover:border-stone-300'
                }`;
                card.innerHTML = `
                    <div class="flex justify-between items-center">
                        <span class="text-xs font-bold text-slate-800">${f.name}</span>
                        <span class="text-xs font-bold text-brand-700">${addPrice > 0 ? '+' + formatARS(addPrice) : 'Incluida'}</span>
                    </div>
                    <span class="block text-[10px] text-brand-600 font-semibold mt-0.5">${f.comp}</span>
                    <p class="text-[11px] text-slate-500 mt-1">${f.desc}</p>
                `;
                container.appendChild(card);
            });
        }

        /* -------------------------------------------------------------------------- */
        /*  GARMENT VISUAL VECTOR (SVG) RENDERER                                       */
        /* -------------------------------------------------------------------------- */
        function selectZone(zone) {
            state.selectedZone = zone;
            document.querySelectorAll('.zone-btn').forEach(btn => {
                btn.classList.remove('active', 'bg-brand-dark', 'text-white');
                btn.classList.add('bg-stone-100', 'text-slate-700');
            });
            const activeBtn = document.getElementById(`zone-btn-${zone}`);
            if (activeBtn) {
                activeBtn.classList.add('active', 'bg-brand-dark', 'text-white');
                activeBtn.classList.remove('bg-stone-100', 'text-slate-700');
            }
        }

        function applySolidColor(hex) {
            state.colors[state.selectedZone] = hex;
            state.patterns[state.selectedZone] = null;
            updateGarmentVisual();
        }

        function applyPattern(patternId) {
            state.patterns[state.selectedZone] = patternId;
            updateGarmentVisual();
        }

        function removeZonePattern() {
            state.patterns[state.selectedZone] = null;
            updateGarmentVisual();
        }

        function setGarmentView(view) {
            state.view = view;
            document.getElementById('view-btn-front').className = view === 'front' 
                ? 'view-btn bg-slate-900 text-white px-4 py-1.5 rounded-lg text-xs font-bold transition shadow-sm flex items-center gap-1.5'
                : 'view-btn text-slate-600 hover:text-slate-900 px-4 py-1.5 rounded-lg text-xs font-semibold transition flex items-center gap-1.5';
            
            document.getElementById('view-btn-back').className = view === 'back' 
                ? 'view-btn bg-slate-900 text-white px-4 py-1.5 rounded-lg text-xs font-bold transition shadow-sm flex items-center gap-1.5'
                : 'view-btn text-slate-600 hover:text-slate-900 px-4 py-1.5 rounded-lg text-xs font-semibold transition flex items-center gap-1.5';

            updateGarmentVisual();
        }

        function updateGarmentVisual() {
            const wrapper = document.getElementById('garment-svg-wrapper');
            let patternDefs = '<defs>';
            PATTERNS_CATALOG.forEach(p => patternDefs += p.svg);
            patternDefs += '</defs>';

            const bodyFill = state.patterns.body ? `url(#p-${state.patterns.body})` : state.colors.body;
            const sleevesFill = state.patterns.sleeves ? `url(#p-${state.patterns.sleeves})` : state.colors.sleeves;
            const collarFill = state.patterns.collar ? `url(#p-${state.patterns.collar})` : state.colors.collar;
            const detailsFill = state.patterns.details ? `url(#p-${state.patterns.details})` : state.colors.details;

            let svgContent = '';

            if (state.garment === 'polera') {
                svgContent = `
                    <svg viewBox="0 0 300 350" class="w-full h-full max-h-[420px]">
                        ${patternDefs}
                        <path d="M 40 80 L 95 60 L 105 130 L 50 145 Z" fill="${sleevesFill}" stroke="#334155" stroke-width="2.5"/>
                        <path d="M 260 80 L 205 60 L 195 130 L 250 145 Z" fill="${sleevesFill}" stroke="#334155" stroke-width="2.5"/>
                        <path d="M 95 60 Q 150 75 205 60 L 215 310 L 85 310 Z" fill="${bodyFill}" stroke="#334155" stroke-width="2.5"/>
                        <path d="M 120 60 Q 150 ${state.view === 'front' ? '95' : '70'} 180 60 Q 150 65 120 60 Z" fill="${collarFill}" stroke="#334155" stroke-width="2"/>
                        ${state.view === 'front' ? `<rect x="160" y="120" width="30" height="35" rx="3" fill="${detailsFill}" stroke="#334155" stroke-width="1.5"/>` : ''}
                    </svg>
                `;
            } else if (state.garment === 'vestido') {
                svgContent = `
                    <svg viewBox="0 0 300 380" class="w-full h-full max-h-[440px]">
                        ${patternDefs}
                        <path d="M 90 50 L 110 50 L 115 110 L 85 110 Z" fill="${sleevesFill}" stroke="#334155" stroke-width="2"/>
                        <path d="M 210 50 L 190 50 L 185 110 L 215 110 Z" fill="${sleevesFill}" stroke="#334155" stroke-width="2"/>
                        <path d="M 110 50 Q 150 65 190 50 L 185 150 L 115 150 Z" fill="${bodyFill}" stroke="#334155" stroke-width="2.5"/>
                        <path d="M 115 150 L 185 150 L 240 360 L 60 360 Z" fill="${bodyFill}" stroke="#334155" stroke-width="2.5"/>
                        <rect x="112" y="145" width="76" height="12" fill="${detailsFill}" stroke="#334155" stroke-width="1.5"/>
                    </svg>
                `;
            } else if (state.garment === 'hoodie') {
                svgContent = `
                    <svg viewBox="0 0 300 360" class="w-full h-full max-h-[420px]">
                        ${patternDefs}
                        <path d="M 30 100 L 90 65 L 105 240 L 50 240 Z" fill="${sleevesFill}" stroke="#334155" stroke-width="2.5"/>
                        <path d="M 270 100 L 210 65 L 195 240 L 250 240 Z" fill="${sleevesFill}" stroke="#334155" stroke-width="2.5"/>
                        <rect x="50" y="240" width="40" height="15" fill="${collarFill}" stroke="#334155" stroke-width="2"/>
                        <rect x="210" y="240" width="40" height="15" fill="${collarFill}" stroke="#334155" stroke-width="2"/>
                        <path d="M 90 65 L 210 65 L 205 320 L 95 320 Z" fill="${bodyFill}" stroke="#334155" stroke-width="2.5"/>
                        <path d="M 110 65 Q 150 20 190 65 Q 150 85 110 65 Z" fill="${collarFill}" stroke="#334155" stroke-width="2"/>
                        ${state.view === 'front' ? `<path d="M 120 220 L 180 220 L 190 280 L 110 280 Z" fill="${detailsFill}" stroke="#334155" stroke-width="2"/>` : ''}
                    </svg>
                `;
            } else {
                svgContent = `
                    <svg viewBox="0 0 300 360" class="w-full h-full max-h-[420px]">
                        ${patternDefs}
                        <rect x="90" y="50" width="120" height="20" rx="3" fill="${collarFill}" stroke="#334155" stroke-width="2"/>
                        <path d="M 90 70 L 145 70 L 135 340 L 85 340 Z" fill="${bodyFill}" stroke="#334155" stroke-width="2.5"/>
                        <path d="M 210 70 L 155 70 L 165 340 L 215 340 Z" fill="${bodyFill}" stroke="#334155" stroke-width="2.5"/>
                    </svg>
                `;
            }

            wrapper.innerHTML = svgContent;
            const garmentObj = (GARMENT_CATALOG[state.category] || []).find(g => g.id === state.garment);
            document.getElementById('canvas-garment-title').textContent = `${garmentObj ? garmentObj.name : 'Prenda'} (${state.category.toUpperCase()})`;
            document.getElementById('canvas-fabric-badge').textContent = `Tela: ${state.fabric.name} (${state.fabric.comp})`;
        }

        /* -------------------------------------------------------------------------- */
        /*  ARTWORK, TEXT & STICKERS ON CANVAS (FABRIC.JS)                            */
        /* -------------------------------------------------------------------------- */
        function addTextToCanvas() {
            const textVal = document.getElementById('custom-text-input').value.trim();
            if (!textVal) return;

            const font = document.getElementById('text-font-family').value;
            const color = document.getElementById('text-color-picker').value;

            const textObj = new fabric.Text(textVal, {
                left: 140,
                top: 160,
                fontFamily: font,
                fill: color,
                fontSize: 24,
                cornerColor: '#c5a059',
                cornerStyle: 'circle'
            });

            fabricCanvas.add(textObj);
            fabricCanvas.setActiveObject(textObj);
            document.getElementById('custom-text-input').value = '';
            showToast('Texto estampado en la prenda');
        }

        function handleImageUpload(e) {
            const file = e.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(f) {
                const data = f.target.result;
                fabric.Image.fromURL(data, function(img) {
                    img.scaleToWidth(100);
                    img.set({ left: 140, top: 150, cornerColor: '#c5a059' });
                    fabricCanvas.add(img);
                    fabricCanvas.setActiveObject(img);
                    showToast('Imagen / Logo añadido');
                });
            };
            reader.readAsDataURL(file);
        }

        function addStickerToCanvas(svgString) {
            fabric.loadSVGFromString(svgString, function(objects, options) {
                const obj = fabric.util.groupSVGElements(objects, options);
                obj.set({ left: 150, top: 150, scaleX: 1, scaleY: 1, cornerColor: '#c5a059' });
                fabricCanvas.add(obj);
                fabricCanvas.setActiveObject(obj);
                showToast('Parche agregado a la prenda');
            });
        }

        function deleteSelectedObject() {
            const active = fabricCanvas.getActiveObject();
            if (active) {
                fabricCanvas.remove(active);
                showToast('Elemento eliminado');
            }
        }

        function bringSelectedForward() {
            const active = fabricCanvas.getActiveObject();
            if (active) fabricCanvas.bringForward(active);
        }

        function clearCanvasArt() {
            fabricCanvas.clear();
            showToast('Lienzo de arte limpiado');
        }

        /* -------------------------------------------------------------------------- */
        /*  SIZING & FIT ADVISOR LOGIC                                                */
        /* -------------------------------------------------------------------------- */
        function selectStandardSize(size) {
            state.selectedSize = size;
            document.querySelectorAll('.size-btn').forEach(btn => {
                btn.classList.remove('active', 'border-brand-gold', 'bg-brand-gold', 'text-slate-950', 'shadow-sm');
                btn.classList.add('border-stone-300', 'text-slate-700');
            });
            event.currentTarget.classList.add('active', 'border-brand-gold', 'bg-brand-gold', 'text-slate-950', 'shadow-sm');
            event.currentTarget.classList.remove('border-stone-300', 'text-slate-700');

            document.getElementById('summary-size-tag').textContent = `Talla: ${size}`;
            calculateFitAdvisor();
        }

        function calculateFitAdvisor() {
            const bust = parseFloat(document.getElementById('meas-bust').value || 0);
            const waist = parseFloat(document.getElementById('meas-waist').value || 0);
            const advisorText = document.getElementById('fit-advisor-text');

            if (bust > 0 || waist > 0) {
                let recSize = 'M';
                if (bust > 0 && bust < 86) recSize = 'XS / S';
                else if (bust >= 86 && bust <= 96) recSize = 'M';
                else if (bust > 96 && bust <= 106) recSize = 'L';
                else if (bust > 106) recSize = 'XL / XXL';

                advisorText.innerHTML = `<strong class="text-brand-700">Calce Recomendado: Talla ${recSize}.</strong> Medidas guardadas para confección.`;
            } else {
                advisorText.textContent = `Basado en la talla ${state.selectedSize} estándar. Ingrese sus medidas corporales si lo prefiere.`;
            }
        }

        function toggleMeasurementGuide() {
            document.getElementById('guide-modal').classList.toggle('hidden');
        }

        /* -------------------------------------------------------------------------- */
        /*  PRICING & QUOTATION SYSTEM                                                */
        /* -------------------------------------------------------------------------- */
        function updateQuotation() {
            const baseCatPrices = garmentPrices[state.category] || {};
            const basePrice = baseCatPrices[state.garment] || 15000;
            const fabricPrice = fabricPrices[state.fabric.id] || 0;
            
            const artworkCount = fabricCanvas ? fabricCanvas.getObjects().length : 0;
            const artworkTotalPrice = artworkCount * artworkUnitPrice;

            const totalPrice = basePrice + fabricPrice + artworkTotalPrice;

            document.getElementById('canvas-total-price').textContent = formatARS(totalPrice);
            
            const itemsContainer = document.getElementById('quotation-items-list');
            itemsContainer.innerHTML = `
                <span>• Base Prenda: <strong class="text-white">${formatARS(basePrice)}</strong></span>
                <span>• Tela (${state.fabric.name}): <strong class="text-white">+${formatARS(fabricPrice)}</strong></span>
                <span>• Arte/Estampados (${artworkCount}): <strong class="text-white">+${formatARS(artworkTotalPrice)}</strong></span>
            `;
        }

        /* -------------------------------------------------------------------------- */
        /*  ADMIN PRICING CONFIGURATION MODAL                                         */
        /* -------------------------------------------------------------------------- */
        function openPricingModal() {
            // Render garment price inputs
            const garmentsContainer = document.getElementById('pricing-garments-inputs');
            garmentsContainer.innerHTML = '';
            
            for (const [cat, items] of Object.entries(GARMENT_CATALOG)) {
                const header = document.createElement('h5');
                header.className = 'font-bold text-slate-700 capitalize mt-2 mb-1';
                header.textContent = `Categoría: ${cat}`;
                garmentsContainer.appendChild(header);

                items.forEach(g => {
                    const currentPrice = (garmentPrices[cat] && garmentPrices[cat][g.id]) || 15000;
                    const row = document.createElement('div');
                    row.className = 'flex justify-between items-center gap-2 mb-1.5';
                    row.innerHTML = `
                        <span class="text-slate-600">${g.name}</span>
                        <div class="flex items-center gap-1">
                            <span class="text-slate-400">$</span>
                            <input type="number" id="price-g-${cat}-${g.id}" value="${currentPrice}" class="w-28 p-1.5 border border-stone-300 rounded-lg text-right font-semibold">
                        </div>
                    `;
                    garmentsContainer.appendChild(row);
                });
            }

            // Render fabric addon price inputs
            const fabricsContainer = document.getElementById('pricing-fabrics-inputs');
            fabricsContainer.innerHTML = '';
            FABRIC_CATALOG.forEach(f => {
                const currentAddon = fabricPrices[f.id] || 0;
                const row = document.createElement('div');
                row.className = 'flex justify-between items-center gap-2 mb-1.5';
                row.innerHTML = `
                    <span class="text-slate-600">${f.name}</span>
                    <div class="flex items-center gap-1">
                        <span class="text-slate-400">$</span>
                        <input type="number" id="price-f-${f.id}" value="${currentAddon}" class="w-28 p-1.5 border border-stone-300 rounded-lg text-right font-semibold">
                    </div>
                `;
                fabricsContainer.appendChild(row);
            });

            document.getElementById('pricing-artwork-input').value = artworkUnitPrice;
            document.getElementById('pricing-modal').classList.remove('hidden');
        }

        function closePricingModal() {
            document.getElementById('pricing-modal').classList.add('hidden');
        }

        function savePricingConfiguration() {
            // Save garment prices
            for (const cat of Object.keys(GARMENT_CATALOG)) {
                GARMENT_CATALOG[cat].forEach(g => {
                    const input = document.getElementById(`price-g-${cat}-${g.id}`);
                    if (input) {
                        if (!garmentPrices[cat]) garmentPrices[cat] = {};
                        garmentPrices[cat][g.id] = parseFloat(input.value) || 0;
                    }
                });
            }

            // Save fabric prices
            FABRIC_CATALOG.forEach(f => {
                const input = document.getElementById(`price-f-${f.id}`);
                if (input) {
                    fabricPrices[f.id] = parseFloat(input.value) || 0;
                }
            });

            // Save artwork price
            const artInput = document.getElementById('pricing-artwork-input');
            if (artInput) {
                artworkUnitPrice = parseFloat(artInput.value) || 0;
            }

            closePricingModal();
            renderGarmentsGrid();
            renderFabricsList();
            updateQuotation();
            showToast('Tarifas actualizadas correctamente en pesos argentinos');
        }

        /* -------------------------------------------------------------------------- */
        /*  ORDER SUBMISSION & EXPORTS                                                */
        /* -------------------------------------------------------------------------- */
        function openOrderModal() {
            const garmentObj = (GARMENT_CATALOG[state.category] || []).find(g => g.id === state.garment);
            const totalPriceText = document.getElementById('canvas-total-price').textContent;

            document.getElementById('order-summary-title').textContent = `${garmentObj ? garmentObj.name : 'Prenda'} Personalizada`;
            document.getElementById('order-summary-details').textContent = `Categoría: ${state.category.toUpperCase()} | Talla: ${state.selectedSize} | Tela: ${state.fabric.name}`;
            document.getElementById('order-summary-price').textContent = totalPriceText;

            document.getElementById('order-modal').classList.remove('hidden');
        }

        function closeOrderModal() {
            document.getElementById('order-modal').classList.add('hidden');
        }

        function submitCustomOrder(e) {
            e.preventDefault();
            closeOrderModal();
            showToast('¡Presupuesto y diseño enviado con éxito al taller! Nos comunicaremos a la brevedad.');
        }

        function downloadDesignImage() {
            const link = document.createElement('a');
            link.download = `Atelier_Diseño_${Date.now()}.png`;
            link.href = fabricCanvas.toDataURL({ format: 'png' });
            link.click();
            showToast('Imagen del diseño guardada');
        }

        function saveDesignToLocal() {
            const designSnapshot = { state, artwork: fabricCanvas.toJSON() };
            localStorage.setItem('atelier_saved_design', JSON.stringify(designSnapshot));
            showToast('Borrador guardado en el navegador');
        }

        function showToast(msg) {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            toast.className = 'p-3 bg-slate-900 text-amber-100 border border-brand-gold rounded-xl shadow-xl text-xs font-semibold flex items-center gap-2 transition-all duration-300 pointer-events-auto';
            toast.innerHTML = `<i class="fa-solid fa-circle-check text-brand-gold"></i> ${msg}`;
            
            container.appendChild(toast);
            setTimeout(() => {
                toast.classList.add('opacity-0', 'translate-x-10');
                setTimeout(() => toast.remove(), 300);
            }, 3000);
        }
    </script>
</body>
</html>
