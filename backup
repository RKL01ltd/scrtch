var canvases = document.getElementsByClassName("scratchC");
  
  	//alert(canvases.length);
    
  for (let i = 0; i < canvases.length; i++) {
  	var context = canvases[i].getContext("2d");
    var canvasToPass = canvases[i];
    test(canvasToPass, context);
  }
  
  
  //var canvas1 = document.getElementById("scratch1");
  //let context1 = canvas1.getContext("2d");
  
  //var canvas2 = document.getElementById("scratch2");
  //let context2 = canvas2.getContext("2d");
  
  //test(canvas1, context1);
  //test(canvas2, context2);
  
  //alert(document.getElementsByClassName("scratchC").length);


function test(canvas, context){
  const init = () => {
    let gradientColor = context.createLinearGradient(0, 0, 135, 135);
    gradientColor.addColorStop(0, "#35ab9c");
    gradientColor.addColorStop(1, "#46acad");
    context.fillStyle = gradientColor;
    context.fillRect(0, 0, 200, 100);
  };

  //initially mouse X and mouse Y positions are 0
  let mouseX = 0;
  let mouseY = 0;
  let isDragged = false;

  //Events for touch and mouse
  let events = {
    mouse: {
      down: "mousedown",
      move: "mousemove",
      up: "mouseup",
    },
    touch: {
      down: "touchstart",
      move: "touchmove",
      up: "touchend",
    },
  };

  let deviceType = "";

  //Detech touch device
  const isTouchDevice = () => {
    try {
      //We try to create TouchEvent. It would fail for desktops and throw error.
      document.createEvent("TouchEvent");
      deviceType = "touch";
      return true;
    } catch (e) {
      deviceType = "mouse";
      return false;
    }
  };

  //Get left and top of canvas
  let rectLeft = canvas.getBoundingClientRect().left;
  let rectTop = canvas.getBoundingClientRect().top;

  //Exact x and y position of mouse/touch
  const getXY = (e) => {
    mouseX = (!isTouchDevice() ? e.pageX : e.touches[0].pageX) - rectLeft;
    mouseY = (!isTouchDevice() ? e.pageY : e.touches[0].pageY) - rectTop;
  };

  isTouchDevice();
  //Start Scratch
  canvas.addEventListener(events[deviceType].down, (event) => {
    isDragged = true;
    //Get x and y position
    getXY(event);
    scratch(mouseX, mouseY);
  });

  //mousemove/touchmove
  canvas.addEventListener(events[deviceType].move, (event) => {
    if (!isTouchDevice()) {
      event.preventDefault();
    }
    if (isDragged) {
      getXY(event);
      scratch(mouseX, mouseY);
    }
  });

  //stop drawing
  canvas.addEventListener(events[deviceType].up, () => {
    isDragged = false;
  });

  //If mouse leaves the square
  canvas.addEventListener("mouseleave", () => {
    isDragged = false;
  });

  const scratch = (x, y) => {
    //destination-out draws new shapes behind the existing canvas content
    context.globalCompositeOperation = "destination-out";
    context.beginPath();
    //arc makes circle - x,y,radius,start angle,end angle
    context.arc(x, y, 12, 0, 2 * Math.PI);
    context.fill();
  };

  //window.onload = init();
  init();

}
