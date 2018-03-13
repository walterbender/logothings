#Poly

Here are some notes on using a general polygon procedure. Introduction
is not yet ready.

A Turtle makes regular polygons and star polygons with the `poly` procedure.

<pre>
to poly :side :angle
poly1 :side :angle heading
end

to poly1 :side :angle :start
fd :side rt :angle
if heading = :start [stop]
poly1 :side :angle :start
end
</pre>

Here are the same polygon shapes with a change in pen size and color.

Reminder: `poly 100 90` (or other angle) is run after changing pen
size and color.

<pre>
setpensize 30
setc "red
setpensize 20
setc "blue
setpensize 10
setc "yellow
setpensize 5
setc "green
The design on the lower right needed more.
setpensize 1
setc "red
</pre>