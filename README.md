# Calculus 1 Module: Derivatives
This README is for the Derivatives section developed by Zach Diaks (zdiaks@mathworks.com) as handed off to Training Services. The purpose of this document is to outline the contents in each section including the written examples and interactive visuals. Code will be mentioned if there is anything non-obvious going on. Future work is also outlined here. 

The main confluence page for this project lives here: https://confluence.mathworks.com/display/MCC/Calculus+I+module?src=contextnavpagetreemode

# Sections
## Definition
This section introduces the derivative as an operator which acts on one function to produce another. After defining the derivative, there is a slide-show style break-down of the definition to motivate the derivative as the slope of a function at a given point. The user should read a point in the numbered list and then change the slider to match that number. Changing the slider updates the view of the plot. This plot serves to provide a visual aid to allow the user to visualize the derivative as slope. This plot makes use of the [getLinApprox](#getLinApprox) function. 

### Try it
The first example has the learner use a slider to tune the value of h in the definition of the derivative to show how the slope between two points on a function converges to a tangent line when the limit as h approaches zero is applied. The next example evaluates the definition of the derivative for y = 6 + cos(x) - 32/5 * exp(-x/5) since this is a nice "bumpy" function. The learner is prompted to take note of the sign and magnitude of this value. 

*I would consider using [getLinApprox](getLinApprox) to add a tangent line to help the user visualize the derivative as slope. To see an example of this, see the "Locating Extrema" section*

## Notations
In this section, three standard notations for derivatives are introduced:
* f'(x)
* df/dx
* d/dx [f(x)]

A distinction is made between the first two and the last one to mention that the last notation is "operator" notation and refers to the derivative as more of an action than a noun. 

## Methods
### Power Rule
Here, the Power Rule is defined with a walkthrough and a couple of examples in the "Try it" section. The functions were chosen to give the learner experience with taking the derivative of:
* Positive exponents
* Negative exponents
* Fractional exponents
* Constants
### Linearity of the Derivative
This section identifies to the learner that the derivative is a linear operator. The definition uses operator notation to connect the learner with the notation in the "Notations" section. 
### Chain Rule
### Transcendental functions
### Product Rule

## Analyzing functions

## Apply your knowledge

# Revealing Answers to Learner


# Helper functions
## <a name="getLinApprox"></a> getLinApprox
This function is used to create a linear approximation of a function at a given point:
```
function linApprox = getLinApprox(y,dy,x,h)
        m = subs(dy,x,h);
        linApprox = m*x + (subs(y,x,h) - m*h);
end
```
Here, y is the function, dy is its derivative, x is the symbolic variable that is used for the function, and h is the point that you're trying to approximate around. 

## solveWrapper
This function allows you to use ```vpasolve``` function to search for multiple solutions to a defined equation given a certain interval. This was needed because ```vpasolve``` will only return one solution to an equation if it is non-polynomial. This function simply creates a sliding window which searches for solutions within the window until the window reaches the boundary specified by x2. Currently, the window size is set to 1, but it might be worth adding the window size as an input to the function in the future. Currently, this function is only used in one instance so this might not be necessary. 
```
function solnSpace = solveWrapper(eqn,x,x1,x2)
    % The first assumption should hold since vpa will return the first
    % solution it finds in the interval
    dx = 1; % Limit the range to find all solution
    interval = [x1,x1 + dx];
    solnSpace = [];
    while interval(2) <= x2
        newSoln = vpasolve(eqn,x,interval);
        
        % Add the solution if vpasolve found one, then slide the window
        if isempty(newSoln)
            % Do nothing
        else
            solnSpace = [solnSpace;newSoln];
        end
        interval = interval + dx;
    end
    solnSpace = unique(solnSpace);
end

```
# Future work
Below is a set of things that I would have worked on if I had the time:
* Add graphics for:  
    * The section introduction (Coffee cup plus cooling curve)
    * Pendulum problem
    * Projectile problem
* Add some symbolic math functionality after the Methods section to allow the user to get the most out of MATLAB. 
* Add a small example/section on analyzing graphs of derivatives versus the original function. 
* Section on Limits
* Section on Integrals

# Resources I found helpful

