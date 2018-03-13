# Math Drill and Practice

## Making a Math Drill and Practice Program.

I was working with some kids who wanted to boost their arithmetic
skills and so together we thought through the following project.

We wanted to beef up skills in addition, subtraction, multiplication
and division. One way to do it was to teach the computer how to make
up an exercise, then ask the user to solve the problem, and check the
response with the actual answer.

To analyze the problem we wrote out some sample exercises such as

`6 + x = 12, 13 - x = 6, 5 * x = 25, 30 / x = 6`

To make up one of these problems the computer has to generate two of
the numbers and compute the third.

We decided to start with addition.

## Addition

Logo is equipped with a random number generator. It takes one input
and then selects a number from 0 up to the input.

`make “number1 random 11`

`:number1` is then 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, or 10
and then we make the second number.

`make “number2 random 11`

## Get the answer

Add the two numbers and save the result.

`make “result :num1 + :num2`

So we make a procedure that prepares the three numbers and then states
the problem, asks for answer, checks it against the correct one, and
keeps asking the same question until the user responds with the right
answer.

In fooling around we found that two procedures were needed. One
procedure makes the three numbers. It then turns the job over to an
assistant (subprocedure) to ask the question and insist on getting the
right answer.

<pre>
to add
make "num1 random 11
make "num2 random 11
make "result :num1 + :num2
add2
end

to add2
question (se :num1 [+ x =] :result char 13 [What is x?])
if answer = :num2 [stop]
add2
end
</pre>

Try it, it works.

## Multiplication

Have you ever thought of the relationship between addition and
multiplication? Well, in writing these procedures we saw that the
procedure for multiplying was very similar to addition. The real
difference lay in how the procedure computed the result.

<pre>
to multiply
make “num1 random 11
make “num2 random 11
make "result :num1 * :num2
multiply2
end

to multiply2
question (se :num1 [* x =] :result char 13 [What is x?])
if answer = :num2 [stop]
multiply2
end
</pre>

Try it, it works.

But wait a minute! we noticed that add2 and multiply2 do similar
jobs. From a programming point of view the only difference is whether
a `+` sign or a `*` sign is printed. Is it possible to make one
procedure work for both add and multiply? We could then use that
procedure for subtracting and dividing.

So we make a new procedure which takes an input. The input is either
`+ x` or `* x`.

<pre>
to check :phrase
question (se :num1 :phrase :result char 13 [What is x?])
if answer = :num2 [stop]
check :phrase
end
</pre>

and edit add and multiply.

<pre>
to add
make "num1 random 11
make "num2 random 11
make "result :num1 + :num2
check [ + x =]
end

to multiply
make “num1 random 11
make “num2 random 11
make "result :num1 * :num2
check [* x =]
end
</pre>

They work but I now see another fix I’d like.

## Math: A Superprocedure

We want a superprocedure which calls on add and multiply and
eventually subtract and divide.

<pre>
to math
add
multiply
end
</pre>

So now on to subtraction.

## Subtraction

In this case we wanted to make sure x is always positive. There are
different ways to do this. I chose is to get num1 by adding result and
num2. Thus subtracting num1.

<pre>
To subtract
make “result random 11
make “num2 random 11
make "num1 :result + :num2
check [ - x =]
end
</pre>

Try it.

## Division

Dividing uses the same technique as the subtract procedure. The
divisor is computed from the other two numbers. The difference here is
that we wanted to avoid the possibility of 0 being any of the
numbers. This is accomplished by adding 1 to the random number.

<pre>
to divide
make “result 1 + random 10
make “num2 1 + random 10
make “num1 :result * :num2
check [/ x =]
end
</pre>

## Making the program better

### Setting Limits

The basics check out. But the poor user is forced to keep trying until
arriving at the right answer. Limits were needed. I chose to move on
after the third incorrect answer.

To accomplish this we had to set up a counter initially set to 1.

`make “times 1`

The check procedure would then have the job of keeping tabs on times
and then either stopping the procedure or adding 1 to times and asking
again for the answer.

Here is the new check procedure.

<pre>
to check :phrase
question (se :num1 :phrase :result char 13 [What is x?])

if answer = :num2 [stop]
if :times > 2 [stop]
make “times :times + 1
check :phrase
end
</pre>

### Providing Visual Feedback

For visuals we, of course, use turtles. We played around and made
several shapes or costumes including the words yes, no, answer and
=. To display this much information we used three turtles. Next, we
wanted to show the correct answer and so I drew the ten digits.

As we were debugging, we decided to plan for answers being as large as
9999. Since we used a turtle for each digit in the answer we needed
four turtles. Altogether we used seven turtles. The tricky thing here
was to hide and show turtles at the right times.

Numbers are words and we can take them apart using first and butfirst
etc. By putting the digits in shape cells 1 through 10 and placing 0
in cell 10 we could say setsh first :number. Of course, we would have
to see if first :number were 0. Then the command would be setsh 10.

`showit` displays the answer digits from left to right. Here is Showit
with comments.

<pre>
to showit :number :places ; :places is the list of the four answer turtles.
ask [t2 t3][ st] ; shows answer =
if empty? :number [wait 20 ask [t1 t2 t3 t4 t5 t6 t7] [ht] stop] ; display the answer for 2
seconds, then hide all
tto first :places ;display a digit
ifelse 0 = first :number [setsh 10 st][setsh first :number st]
showit bf :number bf :places ;do the same thing for the next digit
end
</pre>

### The Whole Thing

<pre>
to math
setup
Add
Subtract
Multiply
divide
end

to add
make "times 1
make "num1 random 11
make "num2 random 11
make "result :num1 + :num2
check [ + x =]
end

to multiply
make "times 1
make “num1 random 11
make “num2 random 11
make "result :num1 * :num2
check [* x =]
end

to subtract
make "times 1
make “result random 11
make “num2 random 11
make "num1 :result + :num2
check [ - x =]
end

to divide :result :num2
make "times 1
make “result 1 + random 10
make “num2 1 + random 10
make "num1 :result * :num2
check[ / x =]
end
</pre>

The check procedure looks complicated because the if instructions are
long. I put yes in cell 17 and no in cell 18.

<pre>
to check :phrase
question (se :num1 :phrase :result char 13 [What is x?])
if empty? Answer [stop]
if :num2 = answer [t1, setsh 17 st showit :num2 [t4 t5 t6 t7] stop]
if :times > 2 [t1, setsh 18 st showit :num2 [t4 t5 t6 t7] wait 20 stop]
make "times :times + 1
t1, setsh 18 st wait 10 ht
check :phrase
end

to showit :number :places
ask [t2 t3][ st]
if empty? :number [wait 20 ask [t1 t2 t3 t4 t5 t6 t7] [ht] stop]
tto first :places
ifelse 0 = first :number [setsh 10 st][setsh first :number st]
showit bf :number bf :places
end
</pre>

The setup procedure is only to restore the seven turtles to their
original positions and looks.

<pre>
to setup
ask [t1 t2 t3 t4 t5 t6 t7][ht sety 130]
t1, setx -250
t2, setx 50 setsh 19
t3, setx 85
setsh 20
t4, setx 170
t5, setx 200
t6, setx 230
t7, setx 260
end
</pre>

### More Changes

* Sometimes display the math sentence.
`6 + x = 12, 13 - x = 6, 5 * x = 25, 30 / x = 6`

* Alternate the number of exercises presented.
* Keep track of the hard ones.
* Change the visual feedback. And so on.