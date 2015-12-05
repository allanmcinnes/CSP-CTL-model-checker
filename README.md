# CSP/CTL Model Checker

Explicit state CTL model-checking implemented in CSPm

Note this this model-checker DOES NOT apply CTL formulas to CSP processes!
It is a hack that tricks FDR into performing CTL model-checking of a user
defined finite state machine expressed as several different sets (not a 
labelled transition system, or a CSP process expression). 
    
## Why? Because we can!
    
Machine readable CSP (i.e. the one used to write scripts for FDR and ProBE)
includes an embedded functional programming language. Which happens to have
some pretty good set manipulation facilities. A combination that makes
it particularly good for implementing a CTL model-checker.

This script implements such a CTL model-checker. The model-checker takes as
input a finite state model (expressed as sets of states, transitions, and
labels), and a CTL formula (expressed in an AST-like form), and checks that
the model satisfies the CTL formula.

FDR requires some kind of assertion about a process to be made in order to
trigger the evaluation of a function. In the case of this script, evaluation
of the model-checking function is triggered by performing a trace refinement
(i.e language containment) check to see if the distinguished initial state
(S.0 by convention) is a member of the set of states returned by the
model-checking function. If the initial state *is* in the returned set of
states then the model satisifes the spec, and the corresponding FDR
assertion will succeed. 

See Huth and Ryan, *Logic in Computer Science*, for details of the
algorithm (http://www.cs.bham.ac.uk/research/lics/)

I've included an example model, and several example specifications, to 
demonstrate how all of this works. To run, simply load into FDR, and check
all assertions.

This script demonstrates (if it demonstrates anything at all) both the 
power of the CSPm embedded functional language, and the simplicity of the
CTL model-checking algorithm. And yes, these are somewhat contradictory
points.
