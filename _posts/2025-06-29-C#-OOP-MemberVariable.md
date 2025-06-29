---
layout: post
title: "OOP in C#: Member Variable"
date: 2025-06-29
---
What is a member variable?
A member variable (also called a field) is a variable inside of a class, but outside of a method.

For example, we have a Car class with a field called _model. By convention, we often use a undercore in front of a field name. Ofcourse, you can use any names that you like. We use a private modifier to prevent access from other class, only methods in the Car class can access this variable.

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ClassApp
{
    internal class Car
    {
        private string _model;
        
    }
}


