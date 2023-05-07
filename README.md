Download Link: https://assignmentchef.com/product/solved-phy224-lab4-nonlinear-fitting-methods-ii
<br>
<strong>Nonlinear circuits</strong>

We continue with the curve fitting from the previous exercises, but extend it to powerlaw models. A lightbulb demonstrates various power laws; resistance and radioactive power are both dependent on temperature for black bodies. In this lab, we will examine these relations with the Voltage-Current curve for a lightbulb.

<h1>Background knowledge for exercise 4</h1>

<strong>Python </strong>lists, arrays, numpy, SciPy, PyPlot, curve_fit()

<strong>Error Analysis </strong>Chi squared (<em>χ</em><sup>2</sup>), goodness of the fit <strong>Physics </strong>Ohm’s law. Review this from your first year text.

<h1>1           Introduction</h1>

An incandescent lightbulb works by heating a tungsten filament until it glows. All matter emits electromagnetic radiation, called <em>thermal radiation</em>, when it has a temperature above absolute zero. The simple theoretical material, a <em>blackbody</em>, is one that absorbs all radiation and follows a strict powerlaw:

<em>P </em>= <em>AσT</em><sup>4 </sup><em>,                                                                                          </em>(1)

where <em>σ </em>is the Stefan-Boltzmann constant (5<em>.</em>670373 × 10<sup>−8 </sup>Wm<sup>−2</sup>K<sup>−4</sup>).

Of course, real materials are not ideal blackbodies. The relation for these “grey bodies” adds an emissivity, <em>ε &lt; </em>1,

<em>P </em>= <em>AσεT</em><sup>4 </sup><em>.                                                                                         </em>(2)

The emissivity itself is typically not constant, and depends on temperature through a power law. For tungsten this relation is,

<em>ε</em>(<em>T</em>) = 1<em>.</em>731 × 10<sup>−3</sup><em>T</em><sup>0<em>.</em>6632 </sup><em>.                                                                          </em>(3)

Including the emissivity leads to a power law between <em>power </em>and <em>temperature</em>. There is also a power law for the resistance of the bulb. In the simplest case, it is treated as linear (<em>R </em>∝ <em>T</em>), but for tungsten it is more accurately,

<em>R</em>(<em>T</em>) ∝ <em>T</em><sup>1<em>.</em>209 </sup><em>.                                                                                      </em>(4)

Combining the dependencies on temperature with <em>P </em>= <em>V I </em>and <em>V </em>= <em>IR</em>, a power law can be found between current and voltage. For an ideal black body with a linear relation between resistance and temperature,

<em> .                                                                                           </em>(5)

For a more physically accurate model of tungsten, we expect

<em>I </em>∝ <em>V </em>0<em>.</em>5882                                                                                                                                      (6)

For most of this experiment, we are not concerned with the constant of proportionality. However, when comparing the theoretical curve to your data you might need to define a suitable value.

<h1>2           Analysis of power laws with logarithms</h1>

The tool for analyzing power laws is, again, logarithms. Start with the general power law,

<em>y </em>= <em>ax<sup>b </sup>,                                                                                            </em>(7)

and take the logarithm of both sides,

log(<em>y</em>) = <em>b</em>log(<em>x</em>) + log(<em>a</em>)<em>.                                                                           </em>(8)

Thus, log(<em>y</em>) depends linearly on log(<em>x</em>), with slope <em>b</em>. We can view this linear relation on a log-log plot (logarithmic scales for both <em>x </em>and <em>y</em>).

Linear regression works again, with the same linear model function, except using log(<em>x<sub>i</sub></em>) and log(<em>y<sub>i</sub></em>) as the input data.

<strong>Note</strong>: The same downfalls of using transformations apply as outlined in Exercise 3 (exponential decay). Again, using curve_fit(), we can use a nonlinear function directly as our model function.

<h1>3           The experiment</h1>

We will observe the power law for blackbody radiation through a lightbulb’s voltage-current graph. Set up the Ohm’s Law experiment as in Exercise 2, but with a lightbulb instead of a resistor.

After setting up the apparatus do the following:

<ol>

 <li>Adjust the power supply voltage to its lowest value.</li>

 <li>Wait for the voltage and current to stabilize (it shouldn’t take long).</li>

 <li>Record the voltage and current values.</li>

 <li>Also record the measurement error.</li>

 <li>Repeat this process for at least 15 different values of voltage.</li>

 <li>Save the values in a text file (.txt) and save it to your memory stick</li>

</ol>

<h1>4           The Python program</h1>

You will use your programs to compare the transformation method and the non-linear least-squares method. The best parameters will be found with both methods, and used to plot best fit curves over the data.

The program should be organized as follows:

<ul>

 <li>Import the required functions and modules (numpy, optimize.curve_fit(), matplotlib.pyplot). • Define the model functions (linearized: <em>f</em>(<em>x,a,b</em>) = <em>ax </em>+ <em>b</em>, non–linear: <em>g</em>(<em>x,a,b</em>) = <em>ax<sup>b</sup></em>)</li>

 <li>Load the data and uncertainty measurements using loadtxt().</li>

 <li>Perform the linear regression on (log(<em>x<sub>i</sub></em>)<em>,</em>log(<em>y<sub>i</sub></em>)) using <em>f </em>as the model function.</li>

 <li>Perform the nonlinear regression on (<em>x<sub>i</sub>,y<sub>i</sub></em>) using <em>g </em>as the model function.</li>

 <li>Output both of the power law relations you calculated.</li>

 <li>Plot the errorbars, both curves of best fit, and the theoretical curve. Include a legend for the different curves.</li>

 <li>Plot all the same things on a log–log plot. One way of doing this is with the loglog() function, another way is to call pylab.yscale(‘log’) and pylab.xscale(‘log’) after you make the plot.</li>

</ul>

The a and b parameters in the two model functions represent different parameters in the original, untransformed, model function. Make sure you can convert between the functions correctly to compare the parameters accurately.

Write the program, and run it using the data gathered in the experiment. Save all plots and the parameters you determined.

<strong>Which regression method gave an exponent closer to the expected value? Can you see the difference on the plots?</strong>

<h1>5           Analyzing the quality of the fit</h1>

As covered in previous exercises, there are two ways that we can assess the quality of the fit of our model: variance of the calculated parameters, and the reduced chi-squared statistic.

<h2>5.1         Variance of parameters</h2>

The variance of the parameters is returned by curve_fit() as the diagonal entries in the covariance matrix, p_cov. Recall that the error in measurements is understood as the standard deviation,

<em>a </em>= <em>a</em>˜ ± <em>σ<sub>a </sub>,                                                                                        </em>(9)

where <em>σ<sub>a </sub></em>= <sup>p</sup>Var(<em>a</em>). In the python program, the variance of the first parameter in your model function is given in p_cov[0, 0], the variance of the second parameter in p_cov[1, 1], and so on.

<strong>Modify your program from Section </strong><strong>4 to calculate the standard deviation of the parameters. What values did you find? Does the value of your fitted exponent fall within the range of the blackbody values (</strong><strong>) with your calculated standard deviation. What about in comparison to the expected value for tungsten?</strong>

<h2>5.2         Reduced chi-squared</h2>

Recall that the <em>χ</em><sup>2 </sup>distribution gives a measure of how unlikely a measurement is. The more a model deviates from the measurements, the higher the value of <em>χ</em><sup>2</sup>. But if <em>χ</em><sup>2 </sup>is too small, it’s also an indication of a problem: usually that there weren’t enough samples.

<strong>Add a function to your program to calculate </strong><em>χ</em><sup>2</sup><sub>red</sub><strong>. What values were computed? How would you interpret your results?</strong>