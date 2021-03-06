Lab 4
===========

**Aim:**

1. To find the magnitude spectrum of a PPG signal using DFT.
2. To compute the pulse rate of the PPG signal using DFT.
3. To compute the pulse rate of the PPG signal using an autocorrelation function.
4. To find out the error using both the methods.

Via

1. The Arduino Platform
2. MATLAB


**Data and Code Links**

1. The Arduino Codes can be found [here.](https://github.com/Chanakya-Ekbote/DSP-Lab/tree/master/Lab-03/Code)
---

Discrete Fourier Transform
---

The mathematical expression for calculating the individual frequency components of a signal (DFT) is as follows 

<p align = "center"><a href="https://www.codecogs.com/eqnedit.php?latex=X[k]&space;=&space;\sum&space;_{n&space;=&space;0}^{N-1}x[n]e^{\frac{-2\pi&space;ikn}{N}}\;\:&space;\forall&space;\;\:k&space;\:\varepsilon&space;\:&space;[0,&space;N-1]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?X[k]&space;=&space;\sum&space;_{n&space;=&space;0}^{N-1}x[n]e^{\frac{-2\pi&space;ikn}{N}}\;\:&space;\forall&space;\;\:k&space;\:\varepsilon&space;\:&space;[0,&space;N-1]" title="X[k] = \sum _{n = 0}^{N-1}x[n]e^{\frac{-2\pi ikn}{N}}\;\: \forall \;\:k \:\varepsilon \: [0, N-1]" /></a></p>

The inverse discrete fourier transform (IDFT) is computed as follows:

<p align = "center"><a href="https://www.codecogs.com/eqnedit.php?latex=x[n]&space;=&space;\frac{\sum&space;_{k&space;=&space;0}^{N-1}x[k]e^{\frac{2\pi&space;ikn}{N}}}{N}&space;\;\:&space;\forall&space;\;\:n&space;\:\varepsilon&space;\:&space;[0,&space;N-1]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x[n]&space;=&space;\frac{\sum&space;_{k&space;=&space;0}^{N-1}x[k]e^{\frac{2\pi&space;ikn}{N}}}{N}&space;\;\:&space;\forall&space;\;\:n&space;\:\varepsilon&space;\:&space;[0,&space;N-1]" title="x[n] = \frac{\sum _{k = 0}^{N-1}x[k]e^{\frac{2\pi ikn}{N}}}{N} \;\: \forall \;\:n \:\varepsilon \: [0, N-1]" /></a></p>

Note that both x[n] and X[k] are periodic functions. This can be intuitively thought about by the following thought experiment:

Suppose you have a discrete time finite length signal. If you take the discrete time fourier transform of that, you get a
periodic continuous function in the frequency domain (function repeats with a period of _2pi_). Now, to process this frequency domain component you would have to sample it in discrete intervals in order to store it in the memmory of an electronic device. Hence we would be multiplying the function in the frequency domain with an impulse train, where the interval between pulses is determined by how much you want to sample. Now the inverse fourier transform of an impulse train is an impulse train, however, this would be convolved with the original finite length signal. Hence, due to this convolution, even the original signal is transformed into a discrete time infinite length periodic function. 

<p float="left" align = "center">
  <img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/0e619f9540710747a4fe02c2959c31c1cec3828a" width="480"/>
</p>

Autocorelation Function
---

The mathematical expression for a discrete time autocorelation function in the time domain is: 

<p align = "center"><a href="https://www.codecogs.com/eqnedit.php?latex=R_{xx}[k]&space;=&space;\sum_{m=&space;-inf}^{inf}x[m]x[m-k]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?R_{xx}[k]&space;=&space;\sum_{m=&space;-\infty}^{\infty}x[m]x[m-k]" title="R_{xx}[k] = \sum_{m= -\infty}^{\infty}x[m]x[m-k]" /></a></p>


The normalised autocorelation function is:  

<p align = "center" ><a href="https://www.codecogs.com/eqnedit.php?latex=R_{xx}[k]&space;=&space;\frac{\sum_{m=&space;-inf}^{inf}x[m]x[m-k]}{R_{xx}[0]}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?R_{xx}[k]&space;=&space;\frac{\sum_{m=&space;-\infty}^{\infty}x[m]x[m-k]}{R_{xx}[0]}" title="R_{xx}[k] = \frac{\sum_{m= -\infty}^{\infty}x[m]x[m-k]}{R_{xx}[0]}" /></a></p>

__Properties of the autocorelation function:__

1. The autocorelation function is symmetric about the Y axis.

<p align = "center" ><a href="https://www.codecogs.com/eqnedit.php?latex=R_{xx}[k]&space;=&space;R_{xx}[-k]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?R_{xx}[k]&space;=&space;R_{xx}[-k]" title="R_{xx}[k] = R_{xx}[-k]" /></a></p>

2. The max value computed by the autocorelation function is at the origin. This value is equal to the energy of the signal.

<p align = "center" ><a href="https://www.codecogs.com/eqnedit.php?latex=R_{xx}[0]&space;=&space;\sum_{m&space;=&space;-\infty}^{\infty}x[m]x[m]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?R_{xx}[0]&space;=&space;\sum_{m&space;=&space;-\infty}^{\infty}x[m]x[m]" title="R_{xx}[0] = \sum_{m = -\infty}^{\infty}x[m]x[m]" /></a></p>

3. If the data itself has a period of _T_, then even the autocorelation of the data has a period of _T_. 


#### Intuition for why the autocorelation provides the time period
---

<p float="left" align = "center">
  <img src="https://github.com/Chanakya-Ekbote/DSP-Lab/blob/master/Lab-03/Images/Sin_1.PNG" width="212"/>
  <img src="https://github.com/Chanakya-Ekbote/DSP-Lab/blob/master/Lab-03/Images/Sin_2.PNG" width="212" /> 
  <img src="https://github.com/Chanakya-Ekbote/DSP-Lab/blob/master/Lab-03/Images/Sin_3.PNG" width="212" />
  <img src="https://github.com/Chanakya-Ekbote/DSP-Lab/blob/master/Lab-03/Images/Sin_4.PNG" width="212" />
</p>

&nbsp; &nbsp; &nbsp; _Fig.1_ &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; _Fig.2_ &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  _Fig.3_ &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  _Fig.4_

The figures represent two different infinte length sine waves shifted by an integer multiple of _pi/2_, where the integer increases on moving to the right. From _Fig.1_ we can observe that the two signals are exactly in phase, hence we get a maximum value. In _Fig.2_ the signals are at a phase difference of _pi/2_. Hence the multiplication of these two signals would yeild a value of zero. In _Fig.3_ the signals are at a phase differene of _pi_ which is totally out of phase and the multiplication of these two signals would yeild a local minima. In _Fig.3._ the phase difference between the signals is _3*pi/2._ the multiplication of these two signals would yeild a value of zero. Increasing the phase further would lead to the same signal in _Fig.1_. Hence we have intuitively proved property 3. Hence we can see that the autocorelation is periodic if the signal it operates on is periodic. 

The intuition provided above for an infinite length signal holds true even for a finite duration signal. However it can be observed that an autocorelation function is in increasing function when its computed for function values less than 0, and decreasing for function values greater than 0. This can be attributed to the fact that the number of data points are finite and computing the autocorelation function can only be done by padding zeros at the ends of the signal. Once this padded signal is corelated with itself there will be a time where only zeros values are being multiplied with each other. Hence, we can see that due only a limited number of signal points being present, we obtain that particular shape of the autocorelation function. 


<p float="left" align = "center">
  <img src="https://github.com/Chanakya-Ekbote/DSP-Lab/blob/master/Lab-03/Images/Autocorr.PNG" width="480"/>
</p>
<p align = "center"> <i>Autocorelation of a sine wave.</i></p>

---

#### Arduino code for DFT of PPG Signal

We take all the samples of the signal and pass them through a low pass (moving average) filter to reduce the high frequency noise in the signal. Next we compute the DFT matrix by spliting the caluclations of the real and imaginary part as computing the Euler's reprenetation of complex numbers is difficult. Next, the real and imaginary part of the DFT is obtained by multipying the real and imaginary parts of the DFT Matrix with the data in the time domain. Then, we obtain the magnitude spectra by squaring and adding the real and imaginary parts of the DFT. After that we find out the first index from the origin where we obtain the maximum magnitude of the magnitude spectra which in turn gives you the max frequency component. 

__Pulse Rate (PR) is calculated as:__ 60 * Fs * (first index) / Length of signal

This is in beats per minute. 

__Arduino Code__
```cpp
float data[75] = {-87.17307638, -109.5495333, 11.00037444, ...}; 
float p = 0;
float x[75];
float N = 75;
double w_real[75][75];
double w_imag[75][75];
double X_real[75];
double X_imag[75];
double X_mag_resp[75];
float Pi = 3.14159;
float inex;
float peak;
float PR = 0;

void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);

}

void loop() 
{

  // Moving Average
  for (int i = 0; i< 75; i++)
  { 
    p = 0;
    if (i<8)
      {for(int k=0; k<i; k++)
        {p += data[i-k];
          }
        }
    else
    {for(int j=0; j<8; j++)
      {
        p += data[i-j];
        }
      }
    x[i] = p;
  }

  ///DFT Computation
  for (int k = 0; k < N; k++)
  { 
    X_real[k] = 0;
    X_imag[k] = 0;
    X_mag_resp[k] = 0;
    
    for(int n = 0; n < N; n++)
    {
      w_real[k][n] = 0;
      w_imag[k][n] = 0;
      w_real[k][n] = cos(2 * Pi * k * n / N);
      w_imag[k][n] = -sin(2 * Pi * k * n / N);
      X_real[k] += x[n] * w_real[k][n];
      X_imag[k] += x[n] * w_imag[k][n];
      X_mag_resp[k] += sqrt(X_real[k] * X_real[k] + X_imag[k] * X_imag[k]);
    }
  }

  //Plotting the Magnitude Response
//  for (int n = 0; n < N; n++)
//  {
//    Serial.println(X_mag_resp[n]);
//  }

  //Getting the maximum value
  peak = 0;
  inex = 0;
 
  for (int n = 0; n < N; n++)
  {
    if (peak < X_mag_resp[n])
    {
      peak = X_mag_resp[n];
      inex = n;
    }
   }

  PR = 60 * (N  - inex) * 25 / N;
  Serial.println(PR);
```


__Plots derived from the Arduino Code__

<p float="left" align = "center">
  <img src="https://github.com/Chanakya-Ekbote/DSP-Lab/blob/master/Lab-04/Images/Magnitude%20Response%20DFT.PNG"/>
</p>

<p align = "center"> <i>Magnitude response of the DFT Spectrum.</i></p>

---

#### Arduino code for Autocorrelation of the PPG Signal

We take a window of 75 samples and calculate the autocorelation for these 75 samples, before passing the data through a low pass (moving average) filter and then we also pass the data through a low pass (moving average) filter. This is done to understand how the presence of high frequency components affects the pulse rate or pitch period calculation. We calculate the time period by checking the sample at which the autocorlation reaches its 2nd maxima from the origin (the first one is at the origin iself). To get this 2nd maxima, we can find out the maxima in the data present after the first zero crossing. To find out the zero crossing, we have to make the signal zero mean. Another method is to find the maxima in the data present after after the global minima. (Please note that we are only considering an autocorelation function computed for _t>0_ to maintain causality.) 

__Time Period (TP) is calculated as:__ (Index number of data point of 2nd maxima + 1) * 1/Fs 

Where Fs is the sampling frequency and the assumption is that the index number starts from 0. 

__Pulse Rate (PR) is calculated as:__ 60/ TP

This is in beats per minute.

__Code__
```cpp
float data[75] = {-87.17307638, -109.5495333, 11.00037444, ...}; 
float test_data[75];
float working_data[75];
float average = 0;
float average_1 = 0;
float x =0;
float max_val = 0;
float pre_filtered_zero = 0;
float pre_filter_maxima =0;
float post_filtered_zero =0;
float post_filter_maxima =0;
float auto_corr_pre_moving_average[4][75];
float auto_corr_post_moving_average[4][75];

void setup() 
{
    Serial.begin(9600);
}

void loop() 
{
    average_1 = 0;
    
    for(int p = 0; p < 75; p++)
    {
      average_1 += data[p];   
    }
    
    // FILTERED
    // Moving Average
    for (int i = 0; i< 75; i++)
    { 
    x = 0;
    if (i<8)
      {for(int k=0; k<i; k++)
        {x += data[i-k]; 
          }
        }
    else
    {for(int j=0; j<8; j++)
      {
        x += data[i-j];
        }
      }
    working_data[i] = x/8;
    average+= working_data[i];
    }
    
    // Zero Mean
    for(int p =0; p<75; p++)
    {
      working_data[p] -= (average/75); 
    }

    // Autocorr
    for(int i = 0; i < 75; i++)
    {
    x = 0;
    for(int j = i; j < 75; j++)
    {
      x += working_data[j]*working_data[j-i];
     }
     auto_corr_post_moving_average[0][i] = x;
     }

    // Zero Crossing
    post_filtered_zero = 0;
    for(int i =0; i<75; i++)
    {
      if ((auto_corr_post_moving_average[0][i] * auto_corr_post_moving_average[0][i+1]) <0)
      {
        post_filtered_zero = i+1;
        break;}
      }
    
    
    // 2nd Maxima
    max_val = 0;
    for(int i=post_filtered_zero; i<75; i++)
    {
      if(max_val <auto_corr_post_moving_average[0][i])
      {
        max_val = auto_corr_post_moving_average[0][i];
        post_filter_maxima = i;
       }
     }

    // Printing
    for (int i =0; i< 75; i++)
    {
     Serial.print(auto_corr_post_moving_average[0][i]/auto_corr_post_moving_average[0][0]);
     Serial.print(',');
     Serial.print(post_filter_maxima/25.0);
     Serial.print(',');
     Serial.println(60/(post_filter_maxima/25.0)); 
     }   
  
}

```

__Plots derived from the Arduino Code__

<p float="left" align = "center">
  <img src="https://github.com/Chanakya-Ekbote/DSP-Lab/blob/master/Lab-04/Images/Arduino_Autocorrelation.PNG"/>
</p>

<p align = "center"> <i>Autocorrelation of the filtered PPG data.</i></p>
----


__MATLAB Code__
```MATLAB
clc;
clear all;
close all;

data = load('Exp03_PPG_25hz_75samples.mat');
data = data.x3;
filter_window = 8;
filtered_data = zeros(size(data));
F = 25;

% Moving Average
for i = 1:size(data,2)
    x = 0;
    if i <= filter_window
        x = sum(data(1:i));
    else
        x = sum(data(i-filter_window:i));
    end
    filtered_data(i) = x / filter_window;
end

% DFT and DFT Matrix
dft = fft(filtered_data);
dft_matrix = dftmtx(size(filtered_data,2));
[~, index] = max(abs(dft));


figure;
plot(abs(dft));
xlabel('Frequency');
ylabel('Magnitude');
title('Magnitude Response');

% Pulse Rate
display(60 * index * F/size(filtered_data,2));


% Autocorrelation
corr = xcorr(filtered_data - mean(filtered_data));
corr = corr(76:end);
figure;
plot(corr);
xlabel('Time');
ylabel('Magnitude');
title('Autocorrelation');

% Zero Crossing 
zero_crossing_index = 0;
for i=1:size(corr, 2)
    if corr(i+1) * corr(i) < 0
        zero_crossing_index = i + 1;
        break
    end
end

% Pulse Rate using Autocorrelation
[~, index_corr] = max(corr(zero_crossing_index:end));
index_corr = zero_crossing_index + index_corr;
display(60/(index_corr/25));
```
__Plots derived from the MATLAB Code__
<p float="left" align = "center">
  <img src="https://github.com/Chanakya-Ekbote/DSP-Lab/blob/master/Lab-04/Images/Autocorrelation.PNG" width=400""/>
  <img src="https://github.com/Chanakya-Ekbote/DSP-Lab/blob/master/Lab-04/Images/Magnitude%20Response.PNG" width="400" /> 
</p>

<p align = "center"> <i>The plot on the left is the autorrelation of the original data. The plot on the right is the Magnitude Spectrum of the DFT of the signal.</i></p>



__Pulse Rate calculated by using both DFT as well as Autocorrelation__

| Pulse rate in calculated using DFT  (in BPM)     |  Pulse rate calculated using Autocorrelation  (in BPM)   |  Error (%) | 
| ----------- | ----------- | ----------- |
| 80      | 68.1818      |  17.33 % |

Hence through the experiment, we can conclude that if the sampling rate is very low (as it was in this experiment) we can see that computing PR using DFT is much worse than calculating PR using Autocorrelation. (Note that the same value is obtained when you use write the code in MATLAB or the C variant used by the Arduino boards. 

---




