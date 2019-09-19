# Human and AI Collaboration

[Creating String-Art](./README.md#creating-string-art) is only possible if human and AI work closely together. To understand what that means, let's take a look at all the steps required to create a single portrait:

1. Select and procure the raw materials
2. Assemble the canvas / frame
3. Select and prepare the source image
4. Find the best path to weave the string
5. Manually weave the string
6. Enjoy the final piece of art

Most of those steps are manual work and cannot be easily automated, at least for a private artist.  **Step 4** is the exception. A **narrow AI** specialized in this specific task can outperform the human brain significantly. 

That's where the collaboration takes place. I've created an algorithm and implemented the individual steps in a suite of Python scripts. The algorithm itself is rather straight forward - the secret sauce lies within the many optimizations, stemming from many months of trial and error.

For those of you curious to dig a little deeper, here is an outline of the general algorithm.

## The String-Art Algorithm

One of the aspects that make String-Art challenging is the fact that we are dealing with a severely limit set of shades of gray. Depending on the technique (with or without backlight) and materials used, we can expect to work with 10 to 20 different shades. The more often the string overlaps in a specific point, the darker this area appears. We have to find a path for the string, that resembles the source image as good as possible within those limitations.

How does the algorithm accomplish that? First of all, we calculate for each possible connection between the hooks, which pixels of the image it touches. That's all we need to know to draw an estimation of what an string-art image will look like for a specific set of selected connections by adding them together.

This estimate can be compared to the chosen image that we want to model. The resulting delta tells us, how far off we are at the moment. By selectively adding or removing connections that improve the delta, we are improving the overall quality of the image step by step. I chose to start with a random set of connections, but the results aren't really different compared to starting from scratch.

It was surprising to me, how fast this algorithm leads to reasonable results. Going over all possible connections twice does already create high quality images. Every additional pass only improves the image marginally at best from there on.

When we have reached the desired quality, we do have a set of connections, but not an established path. This is the next step in the process - finding the best sequence to weave the string. A perfect solution to this puzzle is usually not possible. As soon as we have more than 2 hooks with an odd number of connections, we are bound to fail. Since this is no perfect science, we can live with neglecting some of the less important connections and add some additional ones in the background of the image to establish a single path. And that's how the AI makes trade-offs to derive a single path from the ideal set of connections, trying to impact the image quality as little as possible.

And that's basically it. Following those steps, the AI can tell us now, how to weave the string to get the best result it came up with, basically guiding our hand in the process.

## Conclusion

As already mentioned, the devil is in the details and the algorithm includes many small tweaks and optimizations to create those results. Manually selecting and preparing the source image is also quite a lot of work and takes many hours until it is finished. The AI, although narrow, is an important piece of the puzzle. Only by tight collaboration between human and AI, the string-art portraits can be created.

**The real art is more than just the resulting portrait.** It is the process of working together with the AI to get the best results possible. It is tweaking the algorithm, learning from the output and combining human creativity with artificial compute to create something unique. And of course it is the meditative process of assembling the pieces, weaving the string and consciously enjoying the creation.