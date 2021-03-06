.. index

Custom Error Measures
=====================
Custom error measures must inherit from `pycast.errors.BaseErrorMeasure` and implement the following functions:

  - `_calculate(self, startingPercentage, endPercentage)`
  - `local_error(self, originalValue, calculatedValue)`

Code to start with
------------------
To implement your custom error measrue, it is recommended to start with the following example::

    #!/usr/bin/env python
    # -*- coding: UTF-8 -*-
    
    #Copyright (c) 2012 Christian Schwarz
    #
    #Permission is hereby granted, free of charge, to any person obtaining
    #a copy of this software and associated documentation files (the
    #"Software"), to deal in the Software without restriction, including
    #without limitation the rights to use, copy, modify, merge, publish,
    #distribute, sublicense, and/or sell copies of the Software, and to
    #permit persons to whom the Software is furnished to do so, subject to
    #the following conditions:
    #
    #The above copyright notice and this permission notice shall be
    #included in all copies or substantial portions of the Software.
    #
    #THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
    #EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
    #MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
    #NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
    #LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
    #OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
    #WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
    
    from pycast.errors import BaseErrorMeasure
    
    class CustomErrorMeasure(BaseErrorMeasure):
        """Implements your custom error measure.
        
        Please provide some explanation here!
        """
    
        def _calculate(self, startingPercentage, endPercentage):
            """This is the error calculation function that gets called by :py:meth:`BaseErrorMeasure.get_error`.
    
            Both parameters will be correct at this time.
    
            :param Float startingPercentage: Defines the start of the interval. This has to be a value in [0.0, 100.0].
                It represents the value, where the error calculation should be started. 
                25.0 for example means that the first 25% of all calculated errors will be ignored.
            :param Float endPercentage:    Defines the end of the interval. This has to be a value in [0.0, 100.0].
                It represents the vlaue, after which all error values will be ignored. 90.0 for example means that
                the last 10% of all local errors will be ignored.
    
            :return:    Returns a float representing the error.
            :rtype:     Float
    
            :raise:    Raises a :py:exc:`NotImplementedError` if the child class does not overwrite this method.
            """
            ## get the defined subset of error values
            errorValues = self._get_error_values(startingPercentage, endPercentage)
            
            ## Implement the error calculation here!
    
        def local_error(self, originalValue, calculatedValue):
            """Calculates the error between the two given values.
    
            :param Numeric originalValue:    Value of the original data.
            :param Numeric calculatedValue:    Value of the calculated TimeSeries that
                corresponds to originalValue.
    
            :return:    Returns the error measure of the two given values.
            :rtype:     Numeric
    
            :raise:    Raises a :py:exc:`NotImplementedError` if the child class does not overwrite this method.
            """
            ## Implement the local error calculation here!