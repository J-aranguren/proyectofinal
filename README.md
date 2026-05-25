<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Rutas de Entrega</title>
  <style>
    body { font-family: Arial, sans-serif; text-align: center; background: #f4f4f4; }
    h1 { color: #007acc; }
    canvas { border: 1px solid #333; background: white; margin: 20px auto; display: block; }
    button { margin: 10px; padding: 10px; background: #007acc; color: white; border: none; border-radius: 5px; cursor: pointer; }
    button:hover { background: #005f99; }
  </style>
</head>
<body>
  <h1>🚀 Rutas de Entrega</h1>

  <button onclick="dibujarDrone()">Ruta Drone</button>
  <button onclick="dibujarAuto()">Ruta Auto</button>
  <button onclick="dibujarMoto()">Ruta Moto (Uber)</button>

  <canvas id="mapa" width="700" height="500"></canvas>

  <script>
    const canvas = document.getElementById("mapa");
    const ctx = canvas.getContext("2d");

    function limpiar() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
    }

    // Ruta Drone
    function dibujarDrone() {
      limpiar();
      ctx.strokeStyle = "black";
      ctx.beginPath();
      ctx.moveTo(80,100); ctx.lineTo(600,100);
      ctx.lineTo(600,160); ctx.lineTo(80,220);
      ctx.stroke();

      ctx.fillStyle = "blue";
      ctx.beginPath(); ctx.arc(85,95,5,0,2*Math.PI); ctx.fill();
      ctx.beginPath(); ctx.arc(600,95,5,0,2*Math.PI); ctx.fill();
      ctx.beginPath(); ctx.arc(80,215,5,0,2*Math.PI); ctx.fill();

      ctx.fillStyle = "red";
      ctx.fillRect(85-10,95-10,20,20); // dron
    }

    // Ruta Auto
    function dibujarAuto() {
      limpiar();
      const paradas = [[80,100],[300,100],[500,200],[600,350]];
      const kms = [5,8,12];

      ctx.strokeStyle = "black";
      ctx.beginPath();
      for(let i=0;i<paradas.length-1;i++){
        ctx.moveTo(paradas[i][0],paradas[i][1]);
        ctx.lineTo(paradas[i+1][0],paradas[i+1][1]);
      }
      ctx.stroke();

      ctx.fillStyle="blue";
      paradas.forEach(p=>ctx.fillRect(p[0]-5,p[1]-5,10,10));

      ctx.fillStyle="red";
      for(let i=0;i<kms.length;i++){
        let x=(paradas[i][0]+paradas[i+1][0])/2;
        let y=(paradas[i][1]+paradas[i+1][1])/2;
        ctx.fillText(kms[i]+" km",x,y);
      }

      ctx.fillStyle="green";
      ctx.fillRect(paradas[paradas.length-1][0]-10,paradas[paradas.length-1][1]-10,20,20);
    }

    // Ruta Moto estilo Uber
    function dibujarMoto() {
      limpiar();
      const paradas = [[80,100],[250,150],[400,250],[600,350]];
      const kms = [3,6,8];
      const tiempos = [5,7,10];

      ctx.strokeStyle = "black";
      ctx.beginPath();
      for(let i=0;i<paradas.length-1;i++){
        ctx.moveTo(paradas[i][0],paradas[i][1]);
        ctx.lineTo(paradas[i+1][0],paradas[i+1][1]);
      }
      ctx.stroke();

      ctx.fillStyle="blue";
      paradas.forEach(p=>ctx.fillRect(p[0]-5,p[1]-5,10,10));

      ctx.fillStyle="red";
      for(let i=0;i<kms.length;i++){
        let x=(paradas[i][0]+paradas[i+1][0])/2;
        let y=(paradas[i][1]+paradas[i+1][1])/2;
        ctx.fillText(kms[i]+" km - "+tiempos[i]+" min",x,y);
      }

      ctx.fillStyle="purple";
      ctx.fillRect(paradas[paradas.length-1][0]-10,paradas[paradas.length-1][1]-10,20,20);
      ctx.fillText("Pasajero entregado",paradas[paradas.length-1][0]+15,paradas[paradas.length-1][1]);
    }
  </script>
</body>
</html>
