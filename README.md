Codigo de programa: 
Elaborado y exportado de Android estudio le hice para que emule en web ,ya que mi Computador no es suficente bueno paera arrancar el emualador movil que tiene y uni todos l0os coidos que tiene me guide por videos que pondre :

Francisco Rivera. (2022, 14 septiembre). Sistema para gimnasio (PHP, MySQL, Vue, Vuetify) [Vídeo]. YouTube. https://www.youtube.com/watch?v=_LhmaQmGO9o


MoureDev by Brais Moure. (2020, 17 enero). ANDROID STUDIO: COMO Crear una APP (para Principiantes) 📲 [Tutorial] [Vídeo]. YouTube. https://www.youtube.com/watch?v=BQaxPwZWboA



Yo Androide. (2021, 18 febrero). 😎 ANDROID STUDIO DESDE CERO PARA PRINCIPIANTES 2023 | CREAR UNA APLICACION [Vídeo]. YouTube. https://www.youtube.com/watch?v=juO5H1PBeII


<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>AmazonasGYM - Sistema de Reservas para Gimnasios</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <style id="app-style">
    body {
      font-family: 'Montserrat', sans-serif;
      background-color: #f8f9fa;
    }
    
    .gym-gradient {
      background: linear-gradient(90deg, #ff4757 0%, #ff6b81 100%);
    }
    
    .btn-primary {
      background: linear-gradient(90deg, #ff4757 0%, #ff6b81 100%);
      transition: all 0.3s;
    }
    
    .btn-primary:hover {
      transform: translateY(-2px);
      box-shadow: 0 5px 15px rgba(255, 71, 87, 0.4);
    }
    
    .class-card {
      transition: all 0.3s;
      cursor: pointer;
    }
    
    .class-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
    }
    
    .spinner {
      animation: spin 1s linear infinite;
    }
    
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
    
    .modal-backdrop {
      backdrop-filter: blur(5px);
    }
    
    .notification {
      animation: slideIn 0.3s ease forwards;
      transform: translateY(-100%);
    }
    
    @keyframes slideIn {
      to { transform: translateY(0); }
    }
    
    /* Class type colors */
    .yoga { background-color: #6c5ce7; }
    .cardio { background-color: #e84393; }
    .strength { background-color: #f39c12; }
    .hiit { background-color: #e17055; }
    .cycling { background-color: #00b894; }
    
    /* Calendar styles */
    .calendar-day {
      border-radius: 10px;
      transition: all 0.2s;
    }
    
    .calendar-day:hover {
      background-color: #f1f1f1;
    }
    
    .day-selected {
      background-color: #ff4757 !important;
      color: white;
    }
  </style>
</head>
<body class="min-h-screen">
  <!-- Header -->
  <header class="gym-gradient text-white shadow-lg">
    <div class="container mx-auto px-4 py-3 flex items-center justify-between">
      <div class="flex items-center">
        <i class="fas fa-dumbbell text-3xl mr-2"></i>
        <h1 class="text-2xl font-extrabold">FitReserve</h1>
      </div>
      
      <nav class="hidden md:flex space-x-6">
        <a href="javascript:void(0)" class="font-semibold text-white hover:text-gray-200 active-nav" id="nav-home">
          <i class="fas fa-home mr-1"></i> Inicio
        </a>
        <a href="javascript:void(0)" class="font-semibold text-white hover:text-gray-200" id="nav-bookings">
          <i class="fas fa-calendar-check mr-1"></i> Mis Reservas
        </a>
        <a href="javascript:void(0)" class="font-semibold text-white hover:text-gray-200" id="nav-settings">
          <i class="fas fa-cog mr-1"></i> Configuración
        </a>
      </nav>
      
      <button class="md:hidden text-white focus:outline-none" id="mobile-menu-button">
        <i class="fas fa-bars text-xl"></i>
      </button>
    </div>
    
    <!-- Mobile menu -->
    <div class="md:hidden hidden bg-white text-gray-800 p-4 shadow-lg absolute w-full z-10" id="mobile-menu">
      <a href="javascript:void(0)" class="block py-2 font-semibold hover:text-pink-600 active-nav" id="mobile-nav-home">
        <i class="fas fa-home mr-2"></i> Inicio
      </a>
      <a href="javascript:void(0)" class="block py-2 font-semibold hover:text-pink-600" id="mobile-nav-bookings">
        <i class="fas fa-calendar-check mr-2"></i> Mis Reservas
      </a>
      <a href="javascript:void(0)" class="block py-2 font-semibold hover:text-pink-600" id="mobile-nav-settings">
        <i class="fas fa-cog mr-2"></i> Configuración
      </a>
    </div>
  </header>

  <!-- Main content -->
  <main class="container mx-auto px-4 py-8">
    
    <!-- Home page -->
    <div id="home-page" class="page-content">
      <div class="flex flex-col md:flex-row justify-between items-center mb-8">
        <div>
          <h2 class="text-3xl font-bold text-gray-800 mb-2">Reserva tu próxima clase</h2>
          <p class="text-gray-600">Elige entre una variedad de clases y horarios disponibles</p>
        </div>
        
        <div class="flex flex-wrap mt-4 md:mt-0 gap-3">
          <select id="class-type-filter" class="bg-white border border-gray-300 rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-pink-500">
            <option value="all">Todas las clases</option>
            <option value="yoga">Yoga</option>
            <option value="cardio">Cardio</option>
            <option value="strength">Fuerza</option>
            <option value="hiit">HIIT</option>
            <option value="cycling">Cycling</option>
          </select>
          
          <select id="instructor-filter" class="bg-white border border-gray-300 rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-pink-500">
            <option value="all">Todos los instructores</option>
            <option value="ana">Ana Martínez</option>
            <option value="carlos">Carlos Rodríguez</option>
            <option value="maria">María González</option>
            <option value="pablo">Pablo Sánchez</option>
          </select>
        </div>
      </div>
      
      <!-- Calendar Header -->
      <div class="bg-white rounded-t-xl shadow-md p-4 mb-1">
        <div class="flex justify-between items-center">
          <button id="prev-week" class="p-2 rounded-full hover:bg-gray-100">
            <i class="fas fa-chevron-left"></i>
          </button>
          
          <h3 id="current-month" class="text-xl font-bold text-gray-800">Junio 2025</h3>
          
          <button id="next-week" class="p-2 rounded-full hover:bg-gray-100">
            <i class="fas fa-chevron-right"></i>
          </button>
        </div>
        
        <!-- Days of week -->
        <div class="grid grid-cols-7 gap-2 mt-4">
          <div class="calendar-day flex flex-col items-center p-3 cursor-pointer day-selected" data-day="0">
            <span class="text-sm font-medium">Lun</span>
            <span class="text-lg font-bold">10</span>
          </div>
          <div class="calendar-day flex flex-col items-center p-3 cursor-pointer" data-day="1">
            <span class="text-sm font-medium">Mar</span>
            <span class="text-lg font-bold">11</span>
          </div>
          <div class="calendar-day flex flex-col items-center p-3 cursor-pointer" data-day="2">
            <span class="text-sm font-medium">Mié</span>
            <span class="text-lg font-bold">12</span>
          </div>
          <div class="calendar-day flex flex-col items-center p-3 cursor-pointer" data-day="3">
            <span class="text-sm font-medium">Jue</span>
            <span class="text-lg font-bold">13</span>
          </div>
          <div class="calendar-day flex flex-col items-center p-3 cursor-pointer" data-day="4">
            <span class="text-sm font-medium">Vie</span>
            <span class="text-lg font-bold">14</span>
          </div>
          <div class="calendar-day flex flex-col items-center p-3 cursor-pointer" data-day="5">
            <span class="text-sm font-medium">Sáb</span>
            <span class="text-lg font-bold">15</span>
          </div>
          <div class="calendar-day flex flex-col items-center p-3 cursor-pointer" data-day="6">
            <span class="text-sm font-medium">Dom</span>
            <span class="text-lg font-bold">16</span>
          </div>
        </div>
      </div>
      
      <!-- Classes schedule -->
      <div class="bg-white rounded-b-xl shadow-md p-4 mb-8">
        <div id="classes-container" class="space-y-4">
          <!-- Sample classes -->
          <div class="class-card flex flex-col md:flex-row bg-white border rounded-xl overflow-hidden shadow-sm" data-class-type="yoga" data-instructor="ana">
            <div class="yoga w-full md:w-2 flex items-center justify-center p-4 md:p-0">
              <i class="fas fa-spa text-white text-2xl"></i>
            </div>
            <div class="p-4 flex-grow">
              <div class="flex justify-between items-start">
                <div>
                  <h4 class="font-bold text-lg">Yoga Flow</h4>
                  <p class="text-gray-600 text-sm">Ana Martínez</p>
                </div>
                <span class="bg-green-100 text-green-800 text-xs font-medium px-2 py-1 rounded">10 plazas</span>
              </div>
              <div class="flex items-center mt-4 text-sm">
                <div class="flex items-center mr-4">
                  <i class="far fa-clock mr-1 text-gray-600"></i>
                  <span>7:00 - 8:00</span>
                </div>
                <div class="flex items-center">
                  <i class="fas fa-map-marker-alt mr-1 text-gray-600"></i>
                  <span>Sala 2</span>
                </div>
              </div>
            </div>
            <div class="p-4 flex items-center">
              <button class="book-class-btn bg-gray-100 hover:bg-gray-200 text-gray-800 font-semibold py-2 px-4 rounded-lg transition-colors">
                Reservar
              </button>
            </div>
          </div>
          
          <div class="class-card flex flex-col md:flex-row bg-white border rounded-xl overflow-hidden shadow-sm" data-class-type="cardio" data-instructor="carlos">
            <div class="cardio w-full md:w-2 flex items-center justify-center p-4 md:p-0">
              <i class="fas fa-running text-white text-2xl"></i>
            </div>
            <div class="p-4 flex-grow">
              <div class="flex justify-between items-start">
                <div>
                  <h4 class="font-bold text-lg">Zumba</h4>
                  <p class="text-gray-600 text-sm">Carlos Rodríguez</p>
                </div>
                <span class="bg-yellow-100 text-yellow-800 text-xs font-medium px-2 py-1 rounded">3 plazas</span>
              </div>
              <div class="flex items-center mt-4 text-sm">
                <div class="flex items-center mr-4">
                  <i class="far fa-clock mr-1 text-gray-600"></i>
                  <span>9:00 - 10:00</span>
                </div>
                <div class="flex items-center">
                  <i class="fas fa-map-marker-alt mr-1 text-gray-600"></i>
                  <span>Sala 1</span>
                </div>
              </div>
            </div>
            <div class="p-4 flex items-center">
              <button class="book-class-btn bg-gray-100 hover:bg-gray-200 text-gray-800 font-semibold py-2 px-4 rounded-lg transition-colors">
                Reservar
              </button>
            </div>
          </div>
          
          <div class="class-card flex flex-col md:flex-row bg-white border rounded-xl overflow-hidden shadow-sm" data-class-type="strength" data-instructor="maria">
            <div class="strength w-full md:w-2 flex items-center justify-center p-4 md:p-0">
              <i class="fas fa-dumbbell text-white text-2xl"></i>
            </div>
            <div class="p-4 flex-grow">
              <div class="flex justify-between items-start">
                <div>
                  <h4 class="font-bold text-lg">Body Pump</h4>
                  <p class="text-gray-600 text-sm">María González</p>
                </div>
                <span class="bg-green-100 text-green-800 text-xs font-medium px-2 py-1 rounded">15 plazas</span>
              </div>
              <div class="flex items-center mt-4 text-sm">
                <div class="flex items-center mr-4">
                  <i class="far fa-clock mr-1 text-gray-600"></i>
                  <span>18:00 - 19:00</span>
                </div>
                <div class="flex items-center">
                  <i class="fas fa-map-marker-alt mr-1 text-gray-600"></i>
                  <span>Sala 3</span>
                </div>
              </div>
            </div>
            <div class="p-4 flex items-center">
              <button class="book-class-btn bg-gray-100 hover:bg-gray-200 text-gray-800 font-semibold py-2 px-4 rounded-lg transition-colors">
                Reservar
              </button>
            </div>
          </div>
          
          <div class="class-card flex flex-col md:flex-row bg-white border rounded-xl overflow-hidden shadow-sm" data-class-type="hiit" data-instructor="pablo">
            <div class="hiit w-full md:w-2 flex items-center justify-center p-4 md:p-0">
              <i class="fas fa-fire-alt text-white text-2xl"></i>
            </div>
            <div class="p-4 flex-grow">
              <div class="flex justify-between items-start">
                <div>
                  <h4 class="font-bold text-lg">HIIT Training</h4>
                  <p class="text-gray-600 text-sm">Pablo Sánchez</p>
                </div>
                <span class="bg-red-100 text-red-800 text-xs font-medium px-2 py-1 rounded">Completo</span>
              </div>
              <div class="flex items-center mt-4 text-sm">
                <div class="flex items-center mr-4">
                  <i class="far fa-clock mr-1 text-gray-600"></i>
                  <span>20:00 - 21:00</span>
                </div>
                <div class="flex items-center">
                  <i class="fas fa-map-marker-alt mr-1 text-gray-600"></i>
                  <span>Sala 2</span>
                </div>
              </div>
            </div>
            <div class="p-4 flex items-center">
              <button class="bg-gray-300 text-gray-500 font-semibold py-2 px-4 rounded-lg cursor-not-allowed">
                Completo
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- My Bookings page -->
    <div id="bookings-page" class="page-content hidden">
      <h2 class="text-3xl font-bold text-gray-800 mb-2">Mis Reservas</h2>
      <p class="text-gray-600 mb-8">Gestiona tus clases reservadas</p>
      
      <div class="bg-white rounded-xl shadow-md overflow-hidden">
        <div class="p-6">
          <div class="flex justify-between items-center border-b pb-4 mb-4">
            <h3 class="font-bold text-lg">Próximas clases</h3>
            <div class="text-sm font-medium">
              <a href="javascript:void(0)" class="text-pink-600 hover:underline">Ver todas</a>
            </div>
          </div>
          
          <div id="upcoming-bookings" class="space-y-6">
            <!-- Will be filled with upcoming bookings -->
            <div class="border-b pb-6">
              <div class="flex flex-col md:flex-row md:items-center justify-between">
                <div>
                  <h4 class="font-bold text-lg">Yoga Flow</h4>
                  <div class="flex items-center text-sm text-gray-600 mt-1">
                    <div class="mr-3"><i class="far fa-calendar mr-1"></i> Lun, 10 Jun</div>
                    <div class="mr-3"><i class="far fa-clock mr-1"></i> 7:00 - 8:00</div>
                    <div><i class="fas fa-user mr-1"></i> Ana Martínez</div>
                  </div>
                </div>
                <div class="flex mt-4 md:mt-0">
                  <button class="bg-gray-100 hover:bg-gray-200 text-gray-800 font-medium rounded-lg py-2 px-4 mr-2 transition-colors">
                    <i class="fas fa-exchange-alt mr-1"></i> Cambiar
                  </button>
                  <button class="bg-red-100 hover:bg-red-200 text-red-800 font-medium rounded-lg py-2 px-4 transition-colors">
                    <i class="fas fa-times mr-1"></i> Cancelar
                  </button>
                </div>
              </div>
            </div>
            
            <div class="border-b pb-6">
              <div class="flex flex-col md:flex-row md:items-center justify-between">
                <div>
                  <h4 class="font-bold text-lg">Body Pump</h4>
                  <div class="flex items-center text-sm text-gray-600 mt-1">
                    <div class="mr-3"><i class="far fa-calendar mr-1"></i> Mié, 12 Jun</div>
                    <div class="mr-3"><i class="far fa-clock mr-1"></i> 18:00 - 19:00</div>
                    <div><i class="fas fa-user mr-1"></i> María González</div>
                  </div>
                </div>
                <div class="flex mt-4 md:mt-0">
                  <button class="bg-gray-100 hover:bg-gray-200 text-gray-800 font-medium rounded-lg py-2 px-4 mr-2 transition-colors">
                    <i class="fas fa-exchange-alt mr-1"></i> Cambiar
                  </button>
                  <button class="bg-red-100 hover:bg-red-200 text-red-800 font-medium rounded-lg py-2 px-4 transition-colors">
                    <i class="fas fa-times mr-1"></i> Cancelar
                  </button>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Past bookings -->
          <div class="mt-8">
            <div class="flex justify-between items-center border-b pb-4 mb-4">
              <h3 class="font-bold text-lg">Historial de clases</h3>
              <div class="text-sm font-medium">
                <a href="javascript:void(0)" class="text-pink-600 hover:underline">Ver todo</a>
              </div>
            </div>
            
            <div id="past-bookings" class="space-y-4">
              <div class="flex flex-col md:flex-row justify-between text-gray-500">
                <div>
                  <h4 class="font-semibold">Zumba</h4>
                  <div class="text-sm mt-1">3 Jun 2025 • 9:00 - 10:00 • Carlos Rodríguez</div>
                </div>
                <div class="mt-2 md:mt-0">
                  <button class="text-pink-600 hover:underline text-sm font-medium">
                    <i class="fas fa-redo mr-1"></i> Reservar nuevamente
                  </button>
                </div>
              </div>
              
              <div class="flex flex-col md:flex-row justify-between text-gray-500">
                <div>
                  <h4 class="font-semibold">Yoga Flow</h4>
                  <div class="text-sm mt-1">1 Jun 2025 • 7:00 - 8:00 • Ana Martínez</div>
                </div>
                <div class="mt-2 md:mt-0">
                  <button class="text-pink-600 hover:underline text-sm font-medium">
                    <i class="fas fa-redo mr-1"></i> Reservar nuevamente
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Settings page -->
    <div id="settings-page" class="page-content hidden">
      <h2 class="text-3xl font-bold text-gray-800 mb-2">Configuración</h2>
      <p class="text-gray-600 mb-8">Personaliza tus preferencias y opciones</p>
      
      <div class="bg-white rounded-xl shadow-md overflow-hidden">
        <div class="p-6">
          <!-- Profile Section -->
          <h3 class="font-bold text-xl mb-4">Información Personal</h3>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Nombre</label>
              <input type="text" value="Usuario Ejemplo" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500">
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Email</label>
              <input type="email" value="usuario@ejemplo.com" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500">
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Número de Teléfono</label>
              <input type="text" value="+34 600 123 456" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500">
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">ID de Membresía</label>
              <input type="text" value="MEM-2025-1234" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500 bg-gray-100" readonly>
            </div>
          </div>
          
          <!-- Notification Settings -->
          <h3 class="font-bold text-xl mb-4 pt-4 border-t">Preferencias de Notificación</h3>
          <div class="space-y-4 mb-8">
            <div class="flex items-center justify-between">
              <div>
                <h4 class="font-medium">Recordatorios de clases</h4>
                <p class="text-gray-600 text-sm">Recibe recordatorios antes de tus clases</p>
              </div>
              <label class="relative inline-flex items-center cursor-pointer">
                <input type="checkbox" value="" class="sr-only peer" checked>
                <div class="w-11 h-6 bg-gray-200 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-pink-600"></div>
              </label>
            </div>
            
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">Tiempo de recordatorio</label>
              <select class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500">
                <option>15 minutos antes</option>
                <option selected>30 minutos antes</option>
                <option>1 hora antes</option>
                <option>2 horas antes</option>
              </select>
            </div>
            
            <div class="flex items-center justify-between">
              <div>
                <h4 class="font-medium">Notificaciones por correo</h4>
                <p class="text-gray-600 text-sm">Recibe actualizaciones sobre nuevas clases</p>
              </div>
              <label class="relative inline-flex items-center cursor-pointer">
                <input type="checkbox" value="" class="sr-only peer" checked>
                <div class="w-11 h-6 bg-gray-200 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-pink-600"></div>
              </label>
            </div>
          </div>
          
          <!-- Calendar Integration -->
          <h3 class="font-bold text-xl mb-4 pt-4 border-t">Integración de Calendario</h3>
          <div class="space-y-4 mb-8">
            <div class="flex items-center justify-between">
              <div>
                <h4 class="font-medium">Google Calendar</h4>
                <p class="text-gray-600 text-sm">Sincroniza automáticamente las reservas</p>
              </div>
              <label class="relative inline-flex items-center cursor-pointer">
                <input type="checkbox" value="" class="sr-only peer" checked>
                <div class="w-11 h-6 bg-gray-200 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-pink-600"></div>
              </label>
            </div>
            
            <div class="flex items-center justify-between">
              <div>
                <h4 class="font-medium">Outlook Calendar</h4>
                <p class="text-gray-600 text-sm">Sincroniza automáticamente las reservas</p>
              </div>
              <label class="relative inline-flex items-center cursor-pointer">
                <input type="checkbox" value="" class="sr-only peer">
                <div class="w-11 h-6 bg-gray-200 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-pink-600"></div>
              </label>
            </div>
          </div>
          
          <div class="flex justify-end pt-4 border-t">
            <button class="btn-primary text-white font-bold py-2 px-6 rounded-lg">
              Guardar Configuración
            </button>
          </div>
        </div>
      </div>
    </div>
  </main>

  <!-- Booking Modal -->
  <div id="booking-modal" class="fixed inset-0 flex items-center justify-center z-50 hidden">
    <div class="modal-backdrop absolute inset-0 bg-gray-900 bg-opacity-50"></div>
    <div class="bg-white rounded-xl shadow-xl w-full max-w-md mx-4 z-10 overflow-hidden">
      <div class="gym-gradient text-white p-5">
        <h2 class="text-2xl font-bold" id="booking-modal-title">Reservar Clase</h2>
      </div>
      
      <div class="p-6">
        <form id="booking-form">
          <div class="mb-4">
            <label class="block text-sm font-medium text-gray-700 mb-1">Nombre</label>
            <input type="text" value="Usuario Ejemplo" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500">
          </div>
          
          <div class="mb-4">
            <label class="block text-sm font-medium text-gray-700 mb-1">ID de Membresía</label>
            <input type="text" value="MEM-2025-1234" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500 bg-gray-100" readonly>
          </div>
          
          <div class="mb-4">
            <label class="block text-sm font-medium text-gray-700 mb-1">Clase</label>
            <input type="text" id="class-name" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500 bg-gray-100" readonly>
          </div>
          
          <div class="grid grid-cols-2 gap-4 mb-4">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Fecha</label>
              <input type="text" id="class-date" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500 bg-gray-100" readonly>
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Hora</label>
              <input type="text" id="class-time" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500 bg-gray-100" readonly>
            </div>
          </div>
          
          <div class="mt-6 flex justify-end space-x-3">
            <button type="button" id="close-booking-modal" class="bg-gray-100 hover:bg-gray-200 text-gray-800 font-medium rounded-lg py-2 px-4 transition-colors">
              Cancelar
            </button>
            <button type="submit" class="btn-primary text-white font-medium rounded-lg py-2 px-4">
              Confirmar Reserva
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>

  <!-- Confirmation Modal -->
  <div id="confirmation-modal" class="fixed inset-0 flex items-center justify-center z-50 hidden">
    <div class="modal-backdrop absolute inset-0 bg-gray-900 bg-opacity-50"></div>
    <div class="bg-white rounded-xl shadow-xl w-full max-w-md mx-4 z-10 overflow-hidden">
      <div class="bg-green-500 text-white p-5 flex items-center justify-center">
        <div class="bg-white rounded-full p-3">
          <i class="fas fa-check text-green-500 text-2xl"></i>
        </div>
      </div>
      
      <div class="p-6 text-center">
        <h2 class="text-2xl font-bold mb-2">¡Reserva Confirmada!</h2>
        <p class="text-gray-600 mb-6">Tu clase ha sido reservada exitosamente.</p>
        
        <div class="bg-gray-50 rounded-lg p-4 mb-6">
          <div class="font-bold text-lg mb-1" id="confirm-class-name">Yoga Flow</div>
          <div class="text-gray-600" id="confirm-class-details">Lun, 10 Jun • 7:00 - 8:00 • Sala 2</div>
          <div class="text-gray-600 mt-1" id="confirm-instructor">Instructor: Ana Martínez</div>
        </div>
        
        <div class="flex flex-col space-y-3">
          <button class="bg-green-100 text-green-800 font-medium py-2 px-4 rounded-lg flex items-center justify-center">
            <i class="far fa-calendar-plus mr-2"></i> Añadir a Google Calendar
          </button>
          <button class="bg-blue-100 text-blue-800 font-medium py-2 px-4 rounded-lg flex items-center justify-center">
            <i class="far fa-calendar-alt mr-2"></i> Añadir a Outlook
          </button>
          <button id="close-confirmation-modal" class="mt-2 text-gray-600 font-medium">
            Volver al inicio
          </button>
        </div>
      </div>
    </div>
  </div>

  <!-- Notification Toast -->
  <div id="notification-toast" class="fixed top-4 right-4 z-50 bg-white rounded-lg shadow-lg p-4 flex items-start max-w-xs hidden">
    <div class="flex-shrink-0 mr-3">
      <i class="fas fa-check-circle text-green-500 text-xl"></i>
    </div>
    <div>
      <h4 class="font-bold text-gray-800">¡Éxito!</h4>
      <p class="text-gray-600 text-sm" id="notification-message"></p>
    </div>
    <button class="ml-4 text-gray-400 hover:text-gray-600" id="close-notification">
      <i class="fas fa-times"></i>
    </button>
  </div>

  <script id="app-script">
    // DOM elements
    const mobileMenuButton = document.getElementById('mobile-menu-button');
    const mobileMenu = document.getElementById('mobile-menu');
    const homePage = document.getElementById('home-page');
    const bookingsPage = document.getElementById('bookings-page');
    const settingsPage = document.getElementById('settings-page');
    const navHome = document.getElementById('nav-home');
    const navBookings = document.getElementById('nav-bookings');
    const navSettings = document.getElementById('nav-settings');
    const mobileNavHome = document.getElementById('mobile-nav-home');
    const mobileNavBookings = document.getElementById('mobile-nav-bookings');
    const mobileNavSettings = document.getElementById('mobile-nav-settings');
    const classTypeFilter = document.getElementById('class-type-filter');
    const instructorFilter = document.getElementById('instructor-filter');
    const calendarDays = document.querySelectorAll('.calendar-day');
    const prevWeekBtn = document.getElementById('prev-week');
    const nextWeekBtn = document.getElementById('next-week');
    const currentMonthEl = document.getElementById('current-month');
    const bookButtons = document.querySelectorAll('.book-class-btn');
    const bookingModal = document.getElementById('booking-modal');
    const closeBookingModal = document.getElementById('close-booking-modal');
    const bookingForm = document.getElementById('booking-form');
    const confirmationModal = document.getElementById('confirmation-modal');
    const closeConfirmationModal = document.getElementById('close-confirmation-modal');
    const notificationToast = document.getElementById('notification-toast');
    const closeNotification = document.getElementById('close-notification');
    
    // Mobile menu toggle
    mobileMenuButton.addEventListener('click', () => {
      mobileMenu.classList.toggle('hidden');
    });
    
    // Navigation
    function showPage(page) {
      homePage.classList.add('hidden');
      bookingsPage.classList.add('hidden');
      settingsPage.classList.add('hidden');
      
      document.querySelectorAll('.active-nav').forEach(el => {
        el.classList.remove('active-nav');
      });
      
      if (page === 'home') {
        homePage.classList.remove('hidden');
        navHome.classList.add('active-nav');
        mobileNavHome.classList.add('active-nav');
      } else if (page === 'bookings') {
        bookingsPage.classList.remove('hidden');
        navBookings.classList.add('active-nav');
        mobileNavBookings.classList.add('active-nav');
      } else if (page === 'settings') {
        settingsPage.classList.remove('hidden');
        navSettings.classList.add('active-nav');
        mobileNavSettings.classList.add('active-nav');
      }
      
      mobileMenu.classList.add('hidden');
    }
    
    navHome.addEventListener('click', () => showPage('home'));
    navBookings.addEventListener('click', () => showPage('bookings'));
    navSettings.addEventListener('click', () => showPage('settings'));
    mobileNavHome.addEventListener('click', () => showPage('home'));
    mobileNavBookings.addEventListener('click', () => showPage('bookings'));
    mobileNavSettings.addEventListener('click', () => showPage('settings'));
    
    // Filter classes
    function filterClasses() {
      const classType = classTypeFilter.value;
      const instructor = instructorFilter.value;
      const classCards = document.querySelectorAll('.class-card');
      
      classCards.forEach(card => {
        const cardClassType = card.dataset.classType;
        const cardInstructor = card.dataset.instructor;
        
        const classTypeMatch = classType === 'all' || cardClassType === classType;
        const instructorMatch = instructor === 'all' || cardInstructor === instructor;
        
        if (classTypeMatch && instructorMatch) {
          card.style.display = 'flex';
        } else {
          card.style.display = 'none';
        }
      });
    }
    
    classTypeFilter.addEventListener('change', filterClasses);
    instructorFilter.addEventListener('change', filterClasses);
    
    // Calendar day selection
    calendarDays.forEach(day => {
      day.addEventListener('click', () => {
        calendarDays.forEach(d => d.classList.remove('day-selected'));
        day.classList.add('day-selected');
      });
    });
    
    // Booking modal
    bookButtons.forEach(button => {
      button.addEventListener('click', function() {
        const classCard = this.closest('.class-card');
        const className = classCard.querySelector('h4').textContent;
        const instructor = classCard.querySelector('p').textContent;
        const timeElement = classCard.querySelector('.far.fa-clock').parentNode;
        const time = timeElement ? timeElement.textContent.trim() : '7:00 - 8:00';
        
        // Get selected day from calendar
        const selectedDay = document.querySelector('.day-selected');
        const dayNum = selectedDay.querySelector('.text-lg').textContent;
        const month = currentMonthEl.textContent.split(' ')[0];
        
        // Set modal values
        document.getElementById('class-name').value = className;
        document.getElementById('class-date').value = `${dayNum} ${month}`;
        document.getElementById('class-time').value = time;
        
        // Show modal
        bookingModal.classList.remove('hidden');
      });
    });
    
    closeBookingModal.addEventListener('click', () => {
      bookingModal.classList.add('hidden');
    });
    
    // Form submission
    bookingForm.addEventListener('submit', (e) => {
      e.preventDefault();
      
      // Hide booking modal
      bookingModal.classList.add('hidden');
      
      // Set confirmation details
      const className = document.getElementById('class-name').value;
      const classDate = document.getElementById('class-date').value;
      const classTime = document.getElementById('class-time').value;
      
      document.getElementById('confirm-class-name').textContent = className;
      document.getElementById('confirm-class-details').textContent = `${classDate} • ${classTime} • Sala 2`;
      
      // Show confirmation modal
      confirmationModal.classList.remove('hidden');
    });
    
    closeConfirmationModal.addEventListener('click', () => {
      confirmationModal.classList.add('hidden');
      
      // Show notification
      document.getElementById('notification-message').textContent = 'Tu reserva ha sido confirmada.';
      notificationToast.classList.remove('hidden');
      notificationToast.classList.add('notification');
      
      // Auto hide notification after 5 seconds
      setTimeout(() => {
        notificationToast.classList.add('hidden');
      }, 5000);
    });
    
    closeNotification.addEventListener('click', () => {
      notificationToast.classList.add('hidden');
    });
    
    // Initialize app - load user data from localStorage
    function initializeApp() {
      // Check if user data exists in localStorage
      const userData = localStorage.getItem('userData');
      
      if (!userData) {
        // Create sample user data
        const sampleUserData = {
          name: 'Usuario Ejemplo',
          email: 'usuario@ejemplo.com',
          phone: '+34 600 123 456',
          memberId: 'MEM-2025-1234',
        };
        
        // Store in localStorage
        localStorage.setItem('userData', JSON.stringify(sampleUserData));
      }
    }
    
    // Initialize the application
    initializeApp();
  </script>

  <!-- Footer -->
  <footer class="bg-gray-800 text-white py-8 mt-12">
    <div class="container mx-auto px-4">
      <div class="flex flex-col md:flex-row justify-between">
        <div class="mb-6 md:mb-0">
          <div class="flex items-center mb-4">
            <i class="fas fa-dumbbell text-2xl mr-2 text-pink-500"></i>
            <h3 class="text-xl font-bold">FitReserve</h3>
          </div>
          <p class="text-gray-400 max-w-xs">Tu plataforma para reservar clases y gestionar tu rutina de gimnasio de forma sencilla.</p>
        </div>
        
        <div class="grid grid-cols-2 md:grid-cols-3 gap-8">
          <div>
            <h4 class="text-lg font-semibold mb-4">Servicios</h4>
            <ul class="space-y-2 text-gray-400">
              <li><a href="javascript:void(0)" class="hover:text-pink-400">Reservas</a></li>
              <li><a href="javascript:void(0)" class="hover:text-pink-400">Clases</a></li>
              <li><a href="javascript:void(0)" class="hover:text-pink-400">Entrenadores</a></li>
              <li><a href="javascript:void(0)" class="hover:text-pink-400">Planes</a></li>
            </ul>
          </div>
          
          <div>
            <h4 class="text-lg font-semibold mb-4">Compañía</h4>
            <ul class="space-y-2 text-gray-400">
              <li><a href="javascript:void(0)" class="hover:text-pink-400">Sobre nosotros</a></li>
              <li><a href="javascript:void(0)" class="hover:text-pink-400">Contacto</a></li>
              <li><a href="javascript:void(0)" class="hover:text-pink-400">Blog</a></li>
              <li><a href="javascript:void(0)" class="hover:text-pink-400">Prensa</a></li>
            </ul>
          </div>
          
          <div>
            <h4 class="text-lg font-semibold mb-4">Legal</h4>
            <ul class="space-y-2 text-gray-400">
              <li><a href="javascript:void(0)" class="hover:text-pink-400">Términos</a></li>
              <li><a href="javascript:void(0)" class="hover:text-pink-400">Privacidad</a></li>
              <li><a href="javascript:void(0)" class="hover:text-pink-400">Cookies</a></li>
            </ul>
          </div>
        </div>
      </div>
      
      <div class="border-t border-gray-700 mt-8 pt-6 flex flex-col md:flex-row justify-between items-center">
        <p class="text-gray-400 text-sm">&copy; 2025 FitReserve. Todos los derechos reservados.</p>
        
        <div class="flex space-x-4 mt-4 md:mt-0">
          <a href="javascript:void(0)" class="text-gray-400 hover:text-white text-xl">
            <i class="fab fa-facebook"></i>
          </a>
          <a href="javascript:void(0)" class="text-gray-400 hover:text-white text-xl">
            <i class="fab fa-twitter"></i>
          </a>
          <a href="javascript:void(0)" class="text-gray-400 hover:text-white text-xl">
            <i class="fab fa-instagram"></i>
          </a>
          <a href="javascript:void(0)" class="text-gray-400 hover:text-white text-xl">
            <i class="fab fa-youtube"></i>
          </a>
        </div>
      </div>
    </div>
  </footer>
</body>
</html>
