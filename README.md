<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>I Love You ❤️</title>

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial,sans-serif;
}

body{
    background:black;
    overflow:hidden;
    width:100vw;
    height:100vh;
}



.start{
    position:absolute;
    inset:0;
    display:flex;
    flex-direction:column;
    justify-content:center;
    align-items:center;
    background:black;
    z-index:10;
}

button{
    padding:20px 55px;
    border:none;
    border-radius:20px;
    font-size:32px;
    cursor:pointer;
    color:white;
    background:#ff004c;

    box-shadow:
    0 0 15px #ff004c,
    0 0 40px #ff004c;

    transition:0.3s;
}

button:hover{
    transform:scale(1.08);
}

.hint{
    color:white;
    opacity:0.7;
    margin-top:20px;
    font-size:20px;
}



#scene{
    width:100vw;
    height:100vh;
    position:relative;
    display:none;
}



.word{
    position:absolute;
    color:#ff4d88;
    font-size:12px;
    font-weight:bold;
    opacity:0;
    white-space:nowrap;

    text-shadow:
    0 0 5px #ff4d88,
    0 0 12px #ff4d88,
    0 0 22px #ff0055;

    animation:show 0.8s forwards;
}

@keyframes show{

    from{
        opacity:0;
        transform:scale(0.4);
    }

    to{
        opacity:1;
        transform:scale(1);
    }
}

</style>
</head>
<body>

<div class="start" id="start">
    <button id="btn">I love you</button>
    <div class="hint">Нажми ❤️</div>
</div>

<div id="scene"></div>

<script>

const btn = document.getElementById("btn");
const start = document.getElementById("start");
const scene = document.getElementById("scene");

btn.onclick = () => {

    start.style.display = "none";
    scene.style.display = "block";

    createHeart();
};

function createHeart(){

    const W = window.innerWidth;
    const H = window.innerHeight;

    // Размер сердца
    const scale = Math.min(W, H) / 38;

    let points = [];

    // Слои сердца
    const layers = [];

    // Много плотных слоёв
    for(let i = 1; i >= 0.15; i -= 0.05){
        layers.push(i);
    }

    layers.forEach((layer, layerIndex) => {

        for(let t = 0; t < Math.PI * 2; t += 0.09){

            const x =
            16 * Math.pow(Math.sin(t), 3);

            const y =
            13 * Math.cos(t)
            - 5 * Math.cos(2*t)
            - 2 * Math.cos(3*t)
            - Math.cos(4*t);

            points.push({
                x: x * layer,
                y: y * layer,
                angle: t,
                layer: layerIndex
            });
        }
    });

    // Заполнение по кругу
    points.sort((a,b)=>{

        if(a.layer !== b.layer){
            return a.layer - b.layer;
        }

        return a.angle - b.angle;
    });

    points.forEach((p,index)=>{

        const el = document.createElement("div");

        el.className = "word";

        // КОРОТКИЙ текст
        el.innerText = "i love you";

        const px = W/2 + p.x * scale;
        const py = H/2 - p.y * scale;

        el.style.left = px + "px";
        el.style.top = py + "px";

        // Быстрое плавное появление
        el.style.animationDelay =
        (index * 0.01) + "s";

        scene.appendChild(el);
    });
}
        
        return a.angle - b.angle;
    });

    
    points.forEach((p,index)=>{

        const el = document.createElement("div");

        el.className = "word";
        el.innerText = "i love you";

        const px = W/2 + p.x * scale;
        const py = H/2 - p.y * scale;

        el.style.left = px + "px";
        el.style.top = py + "px";

      
        el.style.animationDelay =
        (index * 0.015) + "s";

        scene.appendChild(el);
    });
}

</script>

</body>
</html>
