//Instructions:
//Place this code in Time Remap of the comp layer you want to control.
//inside this comp, create a null layer named 'task'.
//On the 'task' layer, create a marker(s) called "go".
//If you simply want the internal comp to delay it's start 
     //until called upon, place "go" at frame 1.
//On the outside of this comp, create another marker called "go"
     //at the point at which you want the internal animation
     //to play from it's "go" marker.
//When the trigger marker is reached, the playhead inside this comp is
     //moved to the corresponding marker of null layer 'task'


```
 //...tell it which internal layer will have the markers
 task = comp(name).layer("task");
 //...get the next marker
 n = 0;
 if (marker.numKeys > 0)
 {
	 n = marker.nearestKey(time).index;
	 if (marker.key(n).time > time){
		 n--;
	 }
 }
 if (n == 0){
	 0
 }
 else {
	 m = marker.key(n);
	 theComment = m.comment;
	 t = time - m.time;
	 try{
		 actMarker = task.marker.key(theComment);
		 if (task.marker.numKeys > actMarker.index){
			 tMax = task.marker.key(actMarker.index + 1).time - actMarker.time;
		 }
		 else{
			 tMax = task.outPoint - actMarker.time;
		 }
	 t = Math.min(t, tMax);
	 actMarker.time + t;
	 }
	 catch (err){
	 0
	 }
 }
```


Here’s another way to do the same thing:

```
m = thisComp.layer("some.wav").marker; 
n = 0; 
if (m.numKeys > 0){ 
	n = m.nearestKey(time).index; if (m.key(n).time > time) n--; 
}
t = (n > 0) ? time - m.key(n).time : 0;
seedRandom(n, true);
cm = comp("Footage").marker;
if(cm.numKeys > 0)
{
	i = Math.floor(random(cm.numKeys))+1;
	cm.key(i).time +t;
}
else 0
```