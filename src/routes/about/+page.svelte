
<script lang="ts">
    
    import { onMount } from 'svelte';
    import pic1 from "$lib/img/pic1.jpg";
	import pic2 from "$lib/img/pic2.jpg";
    import pic3 from "$lib/img/pic3.jpg";
    import pic4 from "$lib/img/pic4.png";

    //import {create, attrs, keyframes} from '@stylexjs/stylex';
    let track: HTMLElement;
    
    onMount(() => {
      track = document.getElementById("image-track")!;
    });
    if(typeof window !== 'undefined'){
        window.onmouseup = e => {
            //alert("mouse up");
            if (track) {
                track.dataset.mouseDownAt = "0";
                track.dataset.prevPercentage = track.dataset.percentage;
                //alert(`update ${track.dataset.prevPercentage}`);
            }
        };
        window.onmousedown = e => {
            //alert("mouse down"); 
            if (track) {
                track.dataset.mouseDownAt = e.clientX.toString();
                
                track.dataset.clicked = "1";
                
            }
            
        };
        window.onmousemove = e => {
        
            if(track){
                if(track.dataset.mouseDownAt == "0"){
                   // alert("mouse down at 0");
                    return;
                }
                // alert("mouse move");
                const mouseDelta = parseFloat(track.dataset.mouseDownAt ?? '') - e.clientX, maxDelta = window.innerWidth /2;

                const percentage = (mouseDelta / maxDelta) * -100;
                let newPercentage = parseFloat(track.dataset.prevPercentage ?? '') + percentage;
                newPercentage = Math.min(newPercentage, 0);
                newPercentage = Math.max(newPercentage, -100);
                track.dataset.percentage = percentage.toString();

                
                track.animate({
                    transform: `translate(${newPercentage}%, -50%)`
                }, {duration: 1200, fill: 'forwards'
                })
                //track.style.transform = `translate(${newPercentage}%, -50%)`;
                for(const image of track.getElementsByClassName("image")){
                    (image as HTMLImageElement).animate({
                        objectPosition: `${newPercentage+100}% center`
                    }, {duration: 1200, fill: 'forwards'
                    });
                }
            };
         }
    }
</script>
<!--
<div id = "profile-pic">
    <img src="profile-pic-round.png" alt="" >
</div>
<div id = "text">
    <div id = "line">
        <p class="word">Hello </p>
        <p class="word-fancy">world</p>
    </div>
    <div id = "line">
        <p class = "word">Andrei </p>
        <p class = "word">Maftei</p>
    </div>
</div>-->
<div id = "image-track" data-mouse-down-at = "0" data-prev-percentage = "0" data-clicked = "0" data-percentage = "0">
    <img class="image" src={pic1} alt="" draggable="false"> 
    <img class="image" src={pic2} alt="" draggable="false"> 
    <img class="image" src={pic3} alt="" draggable="false"> 
    <img class="image" src={pic4} alt="" draggable="false"> 
    <img class="image" src={pic1} alt="" draggable="false"> 
    <img class="image" src={pic2} alt="" draggable="false"> 
    <img class="image" src={pic3} alt="" draggable="false"> 
</div>


