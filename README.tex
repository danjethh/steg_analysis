\documentclass{article}
\usepackage{graphicx}
\usepackage{amsmath}
\usepackage{hyperref}
\usepackage{listings}
\usepackage{xcolor}
\usepackage{booktabs}

\title{\textbf{Understanding LSB Manipulation, Steganography, and Feature Extraction for Steganalysis}}
\author{}
\date{}

\begin{document}

\maketitle

\tableofcontents

\section{Introduction}
Steganography is the practice of concealing information within digital media, such as images, in a way that is imperceptible to the human eye. One of the most common techniques for image steganography is \textbf{Least Significant Bit (LSB) manipulation}, where the least significant bits of pixel values are altered to encode hidden data.

This document provides a detailed breakdown of how LSB steganography works, the different types of LSB techniques, how to detect hidden data through steganalysis, and how feature sets help identify manipulated images.

\section{Understanding Image Pixels and Binary Representation}

\subsection{What is a Pixel?}
A \textbf{pixel} is the smallest unit of an image, storing color information in numerical form. In grayscale images, each pixel has a single value between 0 (black) and 255 (white). For color images, each pixel consists of three values: Red, Green, and Blue (RGB), each ranging from 0 to 255.

\begin{table}[h]
\centering
\begin{tabular}{ccc}
\toprule
\textbf{Color} & \textbf{RGB Values} & \textbf{Binary Representation} \
\midrule
Red   & (255, 0, 0)   & (11111111, 00000000, 00000000) \
Green & (0, 255, 0)   & (00000000, 11111111, 00000000) \
Blue  & (0, 0, 255)   & (00000000, 00000000, 11111111) \
Gray  & (128, 128, 128) & (10000000, 10000000, 10000000) \
\bottomrule
\end{tabular}
\caption{Examples of RGB Pixel Values and Their Binary Representations}
\label{tab:rgb}
\end{table}

\subsection{Converting Pixels to Binary}
Computers store image data in binary format. Each color channel of an RGB pixel is represented by an 8-bit binary number. This means that each pixel in an image is composed of 24 bits (8 bits per channel in RGB images).

\begin{verbatim}
Example: Binary Representation of an RGB Pixel
Red:   255 = 11111111
Green: 0   = 00000000
Blue:  64  = 01000000
\end{verbatim}

This binary representation allows us to manipulate specific bits, including the least significant bit (LSB), for steganography.

\section{LSB Manipulation and Data Hiding}

\subsection{How LSB Works}
LSB steganography modifies the least significant bits of pixel values to embed secret data. Since only the last bit is altered, the overall color change is minimal and undetectable to the human eye.

\begin{table}[h]
\centering
\begin{tabular}{ccc}
\toprule
\textbf{Original Pixel Values} & \textbf{Binary Representation} & \textbf{Modified Binary} \
\midrule
128 & 10000000 & 10000001 \
64  & 01000000 & 01000001 \
32  & 00100000 & 00100000 \
16  & 00010000 & 00010001 \
\bottomrule
\end{tabular}
\caption{Example of LSB Modification to Hide 'A' (ASCII 65, Binary: 01000001)}
\label{tab:lsb}
\end{table}

\subsection{Hiding Multiple Characters}
For longer messages, multiple pixels are used. Below is an example of hiding 'AB' (ASCII 65, 66).

\begin{table}[h]
\centering
\begin{tabular}{ccc}
\toprule
\textbf{Original Pixel Values} & \textbf{Binary Representation} & \textbf{Modified Binary} \
\midrule
128 & 10000000 & 10000001 \
64  & 01000000 & 01000001 \
32  & 00100000 & 00100000 \
16  & 00010000 & 00010001 \
8   & 00001000 & 00001000 \
4   & 00000100 & 00000101 \
2   & 00000010 & 00000010 \
1   & 00000001 & 00000001 \
\bottomrule
\end{tabular}
\caption{Example of LSB Modification to Hide 'AB' (ASCII 65, 66)}
\label{tab:lsb_ab}
\end{table}

\subsection{Randomized LSB Matching}
Instead of always incrementing or decrementing the pixel value by 1, LSB matching randomly adds or subtracts 1 when there is a mismatch between the LSB and the message bit. This avoids creating patterns that could be detected by statistical analysis.

\textbf{Example:}
\begin{verbatim}
Original Pixel Value: 128 (10000000)
Message Bit: 1
Random Decision: Subtract 1 -> New Pixel Value: 127 (01111111)
\end{verbatim}

This method helps reduce patterns, making detection harder.

\subsection{Extracting Hidden Data from Steg Images}
Once someone receives the manipulated steg image, they can extract the hidden data by reading the LSBs of the pixel values. Here’s how it works:

\textbf{Reading LSBs}
The tool scans the pixel values and extracts the LSBs.

\begin{table}[h]
\centering
\begin{tabular}{cc}
\toprule
\textbf{Steg Pixel Values} & \textbf{Extracted LSBs} \
\midrule
129 & 1 \
65  & 1 \
32  & 0 \
17  & 1 \
\bottomrule
\end{tabular}
\caption{Extracting LSBs from Steganographic Image}
\label{tab:extract}
\end{table}

These LSBs are concatenated to reconstruct the binary message: 01000001 (which corresponds to 'A').

This method demonstrates how steganography works and how hidden messages can be retrieved efficiently.

\section{Types of LSB Manipulation}

\subsection{LSB Replacement}
LSB replacement is the simplest form of steganography where the least significant bit of a pixel is directly replaced with a bit from the secret message.

\begin{table}[h]
\centering
\begin{tabular}{ccc}
\toprule
\textbf{Original Pixel (Decimal)} & \textbf{Original Pixel (Binary)} & \textbf{Modified Pixel (Binary)} \
\midrule
128 & 10000000 & 10000001 \
64  & 01000000 & 01000001 \
32  & 00100000 & 00100000 \
\bottomrule
\end{tabular}
\caption{Example of LSB Replacement}
\label{tab:lsb_replacement}
\end{table}

In this method, changes occur only in the least significant bits, making the modifications nearly imperceptible to the human eye.

\subsection{LSB Matching}
LSB matching is a variation where instead of directly replacing the LSB, the pixel value is incremented or decremented randomly if the LSB does not match the secret message bit.

\begin{table}[h]
\centering
\begin{tabular}{ccc}
\toprule
\textbf{Original Pixel} & \textbf{Original Binary} & \textbf{Modified Pixel} \
\midrule
128 (10000000) & 10000000 & 127 (01111111) \
200 (11001000) & 11001000 & 201 (11001001) \
\bottomrule
\end{tabular}
\caption{Example of LSB Matching}
\label{tab:lsb_matching}
\end{table}

This technique helps avoid detectable patterns that might be exploited by steganalysis tools.

\subsection{LSB Plane Analysis}
An image can be thought of as multiple bit planes stacked together, where each plane represents a specific bit position of the pixel values. The least significant bit plane (LSBP) and the second least significant bit plane (LSBP2) contain valuable information for steganalysis.

\begin{itemize}
\item \textbf{LSBP (Least Significant Bit Plane)}: The plane that consists of the least significant bits of all pixels in the image. This is where most steganographic changes occur.
\item \textbf{LSBP2 (Second Least Significant Bit Plane)}: The plane consisting of the second least significant bits, which is useful for detecting LSB matching and more advanced steganographic methods.
\end{itemize}

To illustrate the concept of bit planes, consider the following example of an 8-bit grayscale pixel:

\begin{table}[h]
\centering
\begin{tabular}{cccccccc}
\toprule
\textbf{Bit Position} & 7 & 6 & 5 & 4 & 3 & 2 & 1 & 0 \
\midrule
\textbf{Original Pixel (Binary)} & 1 & 0 & 0 & 1 & 0 & 1 & 1 & 0 \
\textbf{LSBP (Bit Plane 0)} & - & - & - & - & - & - & - & 0 \
\textbf{LSBP2 (Bit Plane 1)} & - & - & - & - & - & - & 1 & - \
\bottomrule
\end{tabular}
\caption{Example of LSB and LSBP2 Extraction}
\label{tab:bit_planes}
\end{table}

\subsection{High Correlation Between LSBP and LSBP2}
A high correlation between LSBP and LSBP2 suggests the presence of hidden data, as natural images have a specific statistical distribution that gets disrupted when steganography is applied. The correlation can be measured using autocorrelation functions and statistical analyses.

For example, consider a case where the original and modified LSBP and LSBP2 are analyzed:

\begin{table}[h]
\centering
\begin{tabular}{ccc}
\toprule
\textbf{Pixel Position} & \textbf{Original LSBP} & \textbf{Modified LSBP} \
\midrule
1 & 0 & 1 \
2 & 1 & 1 \
3 & 0 & 1 \
4 & 1 & 1 \
\bottomrule
\end{tabular}
\caption{Example of LSBP Correlation Analysis}
\label{tab:lsbp_correlation}
\end{table}

If there is a significant increase in the similarity between LSBP and LSBP2 after modification, it may indicate the presence of hidden information.

\section{Feature Extraction for Steganalysis}

\subsection{What is a Feature Set?}
A \textbf{feature set} is a collection of measurable properties extracted from an image. These features help detect whether an image contains hidden data by analyzing statistical anomalies introduced by steganography.

Some common features include:
\begin{itemize}
\item \textbf{Histogram analysis}: Detects shifts in pixel intensity distributions.
\item \textbf{Noise analysis}: Identifies unusual noise patterns introduced by LSB modifications.
\item \textbf{Correlation metrics}: Measures the similarity between bit planes to find inconsistencies.
\end{itemize}

These features are used to train machine learning models for steganalysis, enabling automated detection of steganographic content.

\end{document}
