# Mundial
Go to site! You have now a mundial and realistic map!
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mundial</title>
  <!-- Link do Leaflet CSS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    #map {
      height: 100vh; /* O mapa ocupa toda a tela */
    }
    .tooltip-label {
      font-size: 14px;
      font-weight: bold;
      color: #333;
    }
  </style>
</head>
<body>
  <div id="map"></div>

  <!-- Script do Leaflet JS -->
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <script>
    // Inicializar o mapa
    const map = L.map('map').setView([20, 0], 2); // Coordenadas iniciais (Lat, Long), zoom inicial

    // Adicionar camadas de tiles (OpenStreetMap)
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      maxZoom: 18,
      attribution: '© OpenStreetMap contributors'
    }).addTo(map);

    // Exibir marcadores com base no zoom
    function updateMapMarkers() {
      const zoomLevel = map.getZoom();

      // Limpar marcadores existentes
      markers.forEach(marker => map.removeLayer(marker));

      // Adicionar marcadores dependendo do zoom
      if (zoomLevel >= 13) {
        markers.push(
          L.marker([48.8566, 2.3522]).addTo(map).bindTooltip('Paris, França', { permanent: true }),
          L.marker([34.0522, -118.2437]).addTo(map).bindTooltip('Los Angeles, EUA', { permanent: true }),
          L.marker([35.6895, 139.6917]).addTo(map).bindTooltip('Tóquio, Japão', { permanent: true })
        );
      } else if (zoomLevel >= 8) {
        markers.push(
          L.marker([37.7749, -122.4194]).addTo(map).bindTooltip('Califórnia, EUA', { permanent: true }),
          L.marker([51.5074, -0.1278]).addTo(map).bindTooltip('Londres, Inglaterra', { permanent: true }),
          L.marker([-33.8688, 151.2093]).addTo(map).bindTooltip('Sydney, Austrália', { permanent: true })
        );
      } else {
        markers.push(
          L.marker([20, 0]).addTo(map).bindTooltip('Mapa Mundial', { permanent: true })
        );
      }
    }

    // Lista de marcadores
    const markers = [];
    map.on('zoomend', updateMapMarkers);
    updateMapMarkers(); // Chamar a função ao iniciar
  </script>
</body>
</html>
