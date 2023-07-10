---
title: Optics Equations
weight: 210
math: true
menu:
  notes:
    name: Equations
    identifier: notes-optics-equations
    parent: notes-optics
    weight: 10
---

{{<note title="pixel to micron conversion">}}
It is often useful to convert between pixels and microns. This is a simple conversion that can be done with the following formula:
$$
\begin{equation}
\text{microns} = \frac{\text{pixels} \times \text{pixel pitch}}{\text{magnification}} \\
\end{equation}
$$
$$
\begin{equation}
\text{pixels} = \frac{\text{microns} \times \text{magnification}}{\text{pixel pitch}}
\end{equation}
$$
where the pixel pitch is the size of the pixel in microns and the magnification is the magnification of the objective. For example, if we have a 10x objective with a pixel pitch of 6.5 microns, then the conversion is: $$ 1 \text{ pixel} = \frac{6.5 \text{ microns}}{10} = 0.65 \text{ microns} $$ and $$ 1 \text{ micron} = \frac{10 \text{ pixels}}{6.5} = 1.54 \text{ pixels} $$

{{</note>}}