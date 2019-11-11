# LMI-for-Minimizing-the-Maximum-Eigenvalue-of-Matrix

The following are Matlab codes for solving an (Linear Matrix Inequality) LMI problem. This code has been developed for minimizing maximum eigenvalue of a matrix:

clc; clear; close all;

% Variables
t = sdpvar(1);
x1 = sdpvar(1); 
x2 = sdpvar(1);

% Ai (i = 1,2, ..., n) are symmetric matrices
A0 = [1  2 
      2  4];
A1 = [5   3
      3  -2];
A2 = [1   0
      0   4];

% LMI
eta = 0.00000001;
C = [t >= eta];
A = A0 + A1*x1 + A2*x2;
F = [C, A - t*eye(2) <= 0];
optimize(F,t);

% maximum eigenvalues
t = value(t)

% xi
x1 = value(x1)
x2 = value(x2)

% resulted A matrix
A = A0 + A1*x1 + A2*x2;
eigenvalues = eig(A)
