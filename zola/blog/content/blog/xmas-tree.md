+++
title = "X Sin(x) = X-Mas Tree"
date = "2019-12-25"
+++

In this post, I try to create an animation of a christmas tree using Wolfram Language. This idea is originally inspired from the Wolfram community post [here](https://community.wolfram.com/groups/-/m/t/175891).

To begin with, we draw a line...

<center><img src="/images/xmas-tree/xmas-1.png"></center>

And we draw a sine wave...

<center><img src="/images/xmas-tree/xmas-2.png"></center>

We then multiply the two curves...

<center><img src="/images/xmas-tree/xmas-3.png"></center>

We have one half of the tree. Let's flip this to get the other half...

<center><img src="/images/xmas-tree/xmas-4.png"></center>

Now lets plot them together ...

<center><img src="/images/xmas-tree/xmas-5.png"></center>

Now, let's hide the axes...

<center><img src="/images/xmas-tree/xmas-6.png"></center>

And make it upright by rotating 90 degrees clockwise ...

<center><img src="/images/xmas-tree/xmas-7.png"></center>

Let's add some holiday themed colors...

<center><img src="/images/xmas-tree/xmas-8.png"></center>

And let's fill up the background...

<center><img src="/images/xmas-tree/xmas-9.png"></center>

Let's add a bit more styling...

<center><img src="/images/xmas-tree/xmas-10.png"></center>

Adding some snowflakes...

<center><img src="/images/xmas-tree/xmas-11.png"></center>

Finally, we animate everything...

<center><img src="/images/xmas-tree/xmas-12.gif"></center>

Here is the final code that generates the above animation:

```java
Animate[
    Overlay[{
        Rotate[
            Dynamic@ListPlot[
                Table[{RandomReal[]*10, RandomReal[]*10}, {i, 1, 20},PlotMarkers -> Style["*", 18],
                Background -> Black,
                Axes -> False,
                PlotStyle -> White
            ], -90 \[Degree]
        ],
        Rotate[
            Show[
                Plot[x Sin[x + a], {x, 0, 30},
                    PlotStyle -> {Red, Thick, Dashed}
                ],
                Plot[-x Sin[x + a], {x, 0, 30},
                    PlotStyle -> {Darker@Green,
                        Thick, Dashed}
                    ],
                Axes -> False,
                Background -> Transparent
            ], -90 \[Degree]
        ]
    }], {a, 1, 0.01}
]
```

**Merry Christmas :)**

The notebook containing the code can be found on my Github page [here](https://github.com/s4m13337/xmas-tree-2019).
