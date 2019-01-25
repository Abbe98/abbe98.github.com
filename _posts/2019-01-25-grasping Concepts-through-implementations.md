---
layout: post
title: Grasping Concepts through Implementations
description: I sometimes write code to learn things not at all related to code or technical concepts. Here is an example from when I was still in school.
image: https://byabbe.se/assets/python_code.png
---

I sometimes write code to learn things not at all related to code or technical concepts. It can be an implementation of a concept in math or even a 
[Resting Metabolic Rate](https://en.wikipedia.org/wiki/Resting_metabolic_rate) calculator. I used this technique quite a lot back when I was in school.

Below I'm providing an example I found while looking through old hard drives during the holidays. It's Python implementation of the basics of [complex numbers](https://en.wikipedia.org/wiki/Complex_number). The implementation itself is useless as these features are already built into the Python standard library itself but at the time things like this helped me grasp concepts quickly.

<pre><code class="language-python">import math

'''
Implementation of Polar and Cartesian coordinates and conversion between them.

These features exists within the Python standard library, this was meant 
for educational purposes.
'''

class ComplexNumber:
    def __init__(self, real, imaginary, polar = False):
        if polar:
            distance = real
            angle = imaginary
            self.real = distance * math.cos(math.radians(angle))
            self.imaginary = distance * math.sin(math.radians(angle))
        else:
            self.real = real
            self.imaginary = imaginary

    @property
    def distance(self):
        return math.sqrt((self.real ** 2) + (self.imaginary ** 2))
        
    @property
    def angle(self):
        multiplier = 1
        if (self.real < 0):
            # Quadrant 2 or 3
            multiplier = 180
        elif (self.real >= 0 and self.imaginary < 0):
            # Quadrant 4
            multiplier = 360
            
        return math.degrees(math.atan(self.imaginary / self.real)) * multiplier
</code></pre>
