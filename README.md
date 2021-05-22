# Rectangular-Spliterator
Description
Implement RectangularSpliterator methods.
Rectangular Spliterator is a Spliterator that allows to iterate over rectangular 2d array.

Implementation Notes

Spliterator may split into two spliterators, each must cover a half of array.

12345678⇒1256+3478\def\arraystretch{1.5}
   \begin{array}{:c:c:c:c:}
   1 & 2 & 3 & 4 \\
   \hdashline
   5 & 6 & 7 & 8
\end{array}
\Rightarrow
\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   1 & 2  \\
   \hdashline
   5 & 6 
\end{array}
+
\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   3 & 4 \\
   \hdashline
   7 & 8
\end{array}15​26​37​48​​⇒15​26​​+37​48​​

When splitting, source spliterator must cover the second, latter half of an array and new spliterator must cover the first half.

12345678⇒1256(new)+3478(old)\def\arraystretch{1.5}
   \begin{array}{:c:c:c:c:}
   1 & 2 & 3 & 4 \\
   \hdashline
   5 & 6 & 7 & 8
\end{array}
\Rightarrow
\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   1 & 2  \\
   \hdashline
   5 & 6 
\end{array}
(new)+
\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   3 & 4 \\
   \hdashline
   7 & 8
\end{array}
(old)15​26​37​48​​⇒15​26​​(new)+37​48​​(old)

If split parts are not of equal size due to odd length, source iterator makes first part less than second.

123456⇒14(new)+2356(old)\def\arraystretch{1.5}
   \begin{array}{:c:c:c:}
   1 & 2 & 3 \\
   \hdashline
   4 & 5 & 6
\end{array}
\Rightarrow
\def\arraystretch{1.5}
   \begin{array}{:c:}
   1 \\
   \hdashline
   4
\end{array}
(new)+
\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   2 & 3 \\
   \hdashline
   5 & 6
\end{array}
(old)14​25​36​​⇒14​​(new)+25​36​​(old)

When splitting, source spliterator must split the array vertically or horizontally (or one may say, by 1st or 2nd dimension) depending on height/width relation.
If 1st dimension length is greater than 2nd dimension length, then split an array by 1st dimension, otherwise - by 2nd.

12345678⇒1256+3478\def\arraystretch{1.5}
   \begin{array}{:c:c:c:c:}
   1 & 2 & 3 & 4 \\
   \hdashline
   5 & 6 & 7 & 8
\end{array}
\Rightarrow
\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   1 & 2  \\
   \hdashline
   5 & 6 
\end{array}
+
\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   3 & 4 \\
   \hdashline
   7 & 8
\end{array}15​26​37​48​​⇒15​26​​+37​48​​
12345678⇒1234+5678\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   1 & 2 \\
   \hdashline
   3 & 4 \\
   \hdashline
   5 & 6 \\
   \hdashline
   7 & 8 
\end{array}
\Rightarrow
\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   1 & 2  \\
   \hdashline
   3 & 4 
\end{array}
+
\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   5 & 6 \\
   \hdashline
   7 & 8
\end{array}1357​2468​​⇒13​24​​+57​68​​

Spliterator must support splitting unless it covers a single array element.

1234⇒12+34⇒1+2+3+4\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   1 & 2  \\
   \hdashline
   3 & 4
\end{array}
\Rightarrow
\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   1 & 2
\end{array}
+
\def\arraystretch{1.5}
   \begin{array}{:c:c:}
   3 & 4
\end{array}
\Rightarrow
\def\arraystretch{1.5}
   \begin{array}{:c:}
   1
\end{array}
+
\def\arraystretch{1.5}
   \begin{array}{:c:}
   2 
\end{array}
+
\def\arraystretch{1.5}
   \begin{array}{:c:}
   3
\end{array}
+
\def\arraystretch{1.5}
   \begin{array}{:c:}
   4
\end{array}13​24​​⇒1​2​+3​4​⇒1​+2​+3​+4​

Spliterator must properly implement estimateSize method.
You may not consider the case when elements are pulled from spliterator via tryAdvance and then split request occures via trySplit, such a situation should not happen.
Spliterator must be of following characteristscs: IMMUTABLE, ORDERED, SIZED, SUBSIZED, NONNULL.
