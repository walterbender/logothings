# Stacks of Squares

##Trying Out Square

[![Squares 1](../video59.png)]()

Here are the procedures.

<pre>
to square
fd 50 rt 360 / 4
fd 50 rt 360 / 4
fd 50 rt 360 / 4
fd 50 rt 360 / 4
end

to stack
square
fd 50
square
fd 50
square
bk 50 + 50
end

to stackup
stack
rt 90 fd 50 lt 90
stack
rt 90 fd 50 lt 90
end
</pre>

The video continues.

[![Squares 2](../video60.png)](https://youtu.be/cX-wkBXmJFs)

And then

[![Squares 3](../video61.png)](https://youtu.be/lfAzn5hULKk)

The new procedure from the video is:

<pre>
to stackon
repeat 5 [stack fd 10]
end
</pre>

And finally:

[![Squares 4](../video62.png)](https://youtu.be/lQPl9-gcNIM)

<pre>
to stacks
repeat 24 [stackon bk 50 rt 360 / 24]
setc random 256
end
</pre>
