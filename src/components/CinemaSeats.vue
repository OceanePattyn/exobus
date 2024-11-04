<template>
    <div class="container mt-4">
      <h2 class="text-center mb-4">Réservation de places</h2>
      
      <!-- Grille de sièges -->
      <div class="row justify-content-center">
        <div
          v-for="(row, rowIndex) in rows"
          :key="rowIndex"
          class="seat-container mb-2"
        >
          <div
            v-for="(seat, seatIndex) in row"
            :key="seatIndex"
            :class="[
              'seat', 
              seat.reserved ? 'reserved' : 'available'
            ]"
            @click="toggleSeat(seat)"
          >
            {{ seat.seatNumber }}
          </div>
        </div>
      </div>
      
      <!-- Affichage du nombre de sièges réservés -->
      <div class="text-center mt-4">
        <p>Total de sièges réservés : {{ reservedSeatsCount }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue';
  
  // Structure des données
  const rows = ref([
    [
      { seatNumber: '1', reserved: false },
      { seatNumber: '2', reserved: true },
      { seatNumber: '3', reserved: false },
      { seatNumber: '4', reserved: false },
    ],
    [
      { seatNumber: '5', reserved: false },
      { seatNumber: '6', reserved: false },
      { seatNumber: '7', reserved: true },
      { seatNumber: '8', reserved: false },
    ],
    [
      { seatNumber: '9', reserved: false },
      { seatNumber: '10', reserved: false },
      { seatNumber: '11', reserved: true },
      { seatNumber: '12', reserved: false },
    ],
    [
      { seatNumber: '13', reserved: false },
      { seatNumber: '14', reserved: false },
      { seatNumber: '15', reserved: true },
      { seatNumber: '16', reserved: false },
    ],
  ]);
  
  // Fonction pour alterner l'état d'un siège
  function toggleSeat(seat) {
    seat.reserved = !seat.reserved;
  }
  
  // Calcul du nombre de sièges réservés
  const reservedSeatsCount = computed(() =>
    rows.value.flat().filter(seat => seat.reserved).length
  );
  </script>
  
  <style scoped>
  /* Conteneur pour chaque ligne de sièges */
  .seat-container {
    display: flex;
    justify-content: center;
  }
  
  /* Applique un espace au milieu entre les deux blocs de colonnes */
  .seat-container .seat:nth-child(2) {
    margin-right: 50px; /* Espace seulement après la 2e colonne */
  }
  
  /* Style de chaque siège */
  .seat {
    width: 50px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.3s;
    margin: 5px;
  }
  
  .available {
    background-color: lightgray; /* Couleur pour disponible */
    color: black;
  }
  
  .reserved {
    background-color: maroon; /* Couleur pour réservé */
    color: white;
  }
  </style>
  
  