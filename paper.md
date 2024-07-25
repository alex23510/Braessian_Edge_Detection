# Final Submission Braess Edge Detection
Alex Thornton
2024-05-15

# Statement

    TRAN5340M
    Transport Data Science
    Assignment Title:   Braess Edge Detection
    Student ID: 201793166
    Word Count: 3000    
    Lecturer: Dr Malcom Morgan & Dr Robin Lovelace
    Submission Date: 15/5       
    Semester:   2           
    Academic Year:      202324
    Generative AI Category: AMBER

Use of Generative Artificial Intelligence (Gen AI) in this assessment.

I have used Gen AI only for the specific purposes outlined in my
acknowledgements

# Library

- library(knitr)

- library(reticulate)

- library(osmnx)

- library(matplotlib)

- library(Counter)

- library(shapely)

- py -m pip install osmnx

- py -m pip install networkx

- py -m pip install reticulate

- py -m pip install matplotlib

- py -m pip install Counter

- py -m pip install shapely

# Abstract

In 1968, Dietrich Braess demonstrated a counter-intuitive phenomenon now
known as Braess Paradox, where adding a new link to a road network can
degrade overall network performance. This paradox is crucial for urban
and transport planners to understand, yet it remains poorly understood
by the wider public and even amongst professionals. This research
project aims to apply a theoretical model of Braess Paradox to Queens
Road in Leicester, providing insights for transport and urban policy. A
network model was built incorporating edge attributes such as natural
time, usage, capacity, dynamic time, and perceived time. Agents were
generated based on origin-destination pairs and various routing
algorithms. The model was validated using a classic example and then
scaled to more complex scenarios. Our findings indicate that Queens Road
exhibits clear Braessian behaviour, leading to an efficiency loss as
predicted by Roughgarden ,2002. The results suggest that Queens Road
should not be considered a through route and should be pedestrianised to
better serve the local community. These findings underscore the
importance of integrating Braess Paradox considerations into transport
planning.

# Introduction

In 1968 Dietrich Braess published a paper which showed that adding a new
link to a road network might not improve the overall operation of the
network and in some cases may make the network function worse. This
seemingly counter intuitive result became known as Braess Paradox. A
brief generalisable understanding can be formulated as under the
condition of minimal flow, adding a new link to a network can improve
network performance if that link improves travel time. This part is
obvious. However, when increasing flow, a special instance can occur.
This is when the new link reduces the effective capacity of the system
by increasing the flow through low-capacity links, which then reduces
performance. This case can still occur even when flow is dynamically
managed from the perspective of each user.

## Why is it Important in Transport Networks?

There are many things that urban and transport planners should consider
when deciding to add a new road. The logic in Britain has generally been
to build for cars. This has seen traffic saw to record levels and is a
generalisable result from around the world, which unless you’re the
majority shareholder in an oil company is generally seen as a bad thing.
Obviously, there are many components to this and there are many reasons
why traffic has soared. However, anecdotal evidence suggests that Braess
Paradox is generally poorly understood by both the wider public and even
professionals in the transport and urban planning industry.

## What are Potential Practical Applications?

The major practical application is the general principle of reducing
access and speed on and to low-capacity routes, to not lead them to
become overcapacity. This has a myriad of other benefits to. Further to
this, transport planning should not be seen as a one-dimensional
quantitative problem that can be easily and exactly solved with a model,
especially in the case of cars. It should be understood analytically
through the study of a myriad of effects that can be understood
quantitatively, and appreciated qualitatively, recognizing that solving
transport problems exactly for cars is not feasible. As will be
discussed later, predicting braessian edges is an NP hard problem and
there is no computationally sensible generalisable solution on large
scales. What then should be taken from this is a rigorous appreciation
of the quantitative and how to apply that to the qualitative.

## No Exact Generalisable Theoretical Way of Predicting Braessian Edges

The best theoretical work to be done on this topic is often found when
Braess paradox is applied to electrical networks. Its beyond the scope
of this project to discuss why that is. One reason intuitively is that
because the failure of electrical networks is seen as something that can
never be allowed to happen; the same is not true for car networks. The
obvious analogy is with airline safety and car safety.

However, a good example is the work by Roughgarden 2006, which proved
that detecting even the worst manifestations of Braess Paradox is an NP
hard problem. Since then, more substantive work has been done in
electrical networks Manik 2022, which showed that an analogous problem
is computationally solvable un-exactly at least by considering the
rerouting alignment, or in other words how the between centrality
changes when adding and edge. This is the logic that has been taken
forward in finding an approximate solution.

# Aims

This research project seeks to apply a theoretical model of Braess
paradox to a real-world scenario to add to a body of work relating to
the case for a different approach to transport and urban policy. It aims
to add to the list of considerations when deciding the appropriate
function of a road in a network. The questions this project hopes to
answer are, “Should Queens Road be seen as a through route?” and “What
practical takeaways can we observe from this analytical understanding?”

# Literature Review

In their 2022 work Zhuang and Huang considered dynamic traffic
assignment and the effects of junctions on Braess paradox rather than
understanding the network in a simplified set of flows model without
node interactions. They also applied cooperative autonomous vehicles
using applied reinforcement learning. More recently, a study by Gao et
al. (2021) explored the applications of machine learning in predicting
Braess Paradox in transportation networks. They used neural networks to
analyse traffic patterns and identify potential Braessian edges, showing
promising results in improving prediction accuracy and reducing
computational costs.

Manik (2022), found a new topological understanding of Braess paradox
when applied to electrical networks which greatly reduced the
computation cost and reduced the intractability, with an overall
prediction rate of about 90%. This work was built on the work of Shapiro
1987. Colleta and Jaqoud (2016) managed to prove the phenomena on the
British power grid to predict the change in network flows as the result
of adding an edge.

A study by Cohen and Horowitz (1991) examined the impact of network
changes in the city of Stuttgart, Germany. Their findings confirmed that
the addition of new roads led to increased travel times.In another
study, Youn, Gastner, and Jeong (2008) analyzed traffic patterns in
Boston and demonstrated that removing certain roads could actually
improve overall traffic flow.

# Methodology

# Methodological Outline

A network was built which contained edges and nodes. The edges were
assigned the variables natural time, usage, capacity, perceived time and
dynamic time.

- Natural time or nat_time, stores the information about the time it
  takes to get from one end of the edge to another under zero traffic
  flow.
- Usage is the variable which stores total traffic flow across an edge.
- Capacity is the constant which determines how the usage impacts the
  natural time.
- Dynamic time variable computed by a function of natural time, usage,
  and capacity.
- Perceived time is variable which stores the perceived time, which is
  used in one of the algorithms for agent routing. Perceived time is a
  function of dynamic and natural time.