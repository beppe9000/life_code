# Particle Life Simulation
A simple program to simulate attraction/reuplsion forces between many particles

Learn More Here (YouTube video tutorial):
-----------------------------------------------
https://youtu.be/0Kx4Y9TVMGg


Interface
--------------------------------------------------------
![](images/interface.jpg)

Example Results
--------------------------------------------------------
![](images/big_pic.jpg)

Code
----------------
Source code available in both C++ (using openframeworks liberary) and javascript

The javascript code is as simple as this:
```
  <canvas id="life" width="500" height="500"></canvas>
  <script>
    //Hunar Ahmad @ brainxyz
  m=document.getElementById("life").getContext('2d')
  draw=(x,y,c,s)=>{m.fillStyle=c; m.fillRect(x, y, s, s)}
  atoms=[]
  atom=(x,y,c)=>{return{"x":x, "y":y, "vx":0, "vy":0, "color":c}}
  random=()=>{return Math.random()*400+50}
  create=(number, color)=>{ 
  	group=[]
    for(let i=0; i < number; i++){
	    group.push(atom(random(), random(), color))
	    atoms.push(group[i]) 
	}
    return group 
  }
  rule=(atoms1, atoms2, g)=>{
  for(let i=0; i < atoms1.length; i++){
    fx = 0
    fy = 0
    for(let j=0; j < atoms2.length; j++){
      a = atoms1[i]
      b = atoms2[j]
      dx = a.x-b.x
      dy = a.y-b.y
      d = Math.sqrt(dx*dx + dy*dy)
      if(d > 0 && d < 80){
      	F = g * 1/d
        fx += (F * dx)
        fy += (F * dy)
      }
    } 
    a.vx = (a.vx + fx)*0.5
    a.vy = (a.vy + fy)*0.5
    a.x += a.vx
    a.y += a.vy
    if(a.x <= 0 || a.x >= 500){ a.vx *=-1 }
    if(a.y <= 0 || a.y >= 500){ a.vy *=-1 }
    }
  }
  yellow = create(200, "yellow")
  red = create(200, "red")
  green = create(200, "green")
  update=()=>{
    rule(green, green, -0.32)
    rule(green, red, -0.17)
    rule(green, yellow, 0.34)
    rule(red, red, -0.10)
    rule(red, green, -0.34)
    rule(yellow, yellow, 0.15)
    rule(yellow, green, -0.20)
    m.clearRect(0, 0, 500, 500)
    draw(0, 0, "black", 500)
    for(i=0; i<atoms.length; i++){ 
    draw(atoms[i].x, atoms[i].y, atoms[i].color, 5) 
    }
    requestAnimationFrame(update)
  }
  update();
  </script>

```

</br>
