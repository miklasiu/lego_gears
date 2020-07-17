# lego_gears
OpenSCAD lib to create lego compatible gears.

I just got 3d printer kit and I need something to test it on. Gears are always useful...


lego_gear(s, flat_surface=true, central_axle=true, solid=false, stud_hole_tolerance=0.00, axle_hole_tolerance=0.05)

parameters:
s - size in lego brick length. Spurs count is s*16.
standard sizes are 0.5 (8 spurs), 1 (16 spurs), 1.5 (24 spurs), 2.5 (40 spurs). Other down to 0.0625 (1 spur) are possible. There is no restriction on that parameter. Be wise. 8 spur gear is the minimum for the axle hole to make sense. Smaller are possible - not sure if usable though.
flat surface - if set to true will create big flat space on both sides of the gear so it prints better - there will be less support required.
central axle - create a hole for the central axle. If set to false there will be none so you can create a custom one - to interface with non-lego stuff
solid - if set to true - create no additional spur or axle holes off the center. Implies "flat_surface".
stud_hole_tolerance - offset from 4.8/6.2mm standard. Positive values give bigger holes.
axle_hole_tolerance - offset from 4.8 standard. Default is 0.05 (4.75mm). Positive values give bigger holes.


lego_axle(m=1, hole=false, tolerance=0.05)

m - size in lego bricks (8mm) total length will be m*8-0.15mm
hole - make the axle to be used to make holes in other objects with it. Basically tolerance make the axle bigger if set to true. If set to flase the tolerance makes the axle smaller
tolerance - offset to apply to cross section dimension. Default is 0.05 giving 4.75 mm axles and 4.85mm holes


non-lego:
rounded_square(size, r=0.2)

size - like for the square module
r - radius of the rounding circle


example:
for (s = [0.5:1:2.5]) translate([s*s*8,0,0]) rotate([0,0,22.5*(s-0.5)]) lego_gear(s);
for (s = [1:1:2]) translate([-s*s*8-2,0,0]) rotate([0,0,22.5*s/2]) lego_gear(s, flat_surface=false);
