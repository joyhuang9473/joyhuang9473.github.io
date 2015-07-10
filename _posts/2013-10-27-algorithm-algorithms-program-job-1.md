---
layout: post
title: '演算法 Algorithms : 程式作業1'
date: 2013-10-27 13:31
comments: true
tags: 
---
For two points p and q in the plane, we say that p dominates q if both x and y coordinates of p are greater than that of q respectively. Given a set S of n points, the rank of a point p in S is the number of points in S dominated by p. We want to find the rank of every point in S. A naïve algorithm needs O(n^2) time. Design a faster algorithm for this problem.

Input

The first line of input contains a single positive integer ( < 20 ), the number of test cases. Each test case starts with a line containing a single integer n, the number of points in the plane. This line is followed by n lines, indicates the x and y coordinates for each points, p1, p2… pn. No integer in the input is greater than 224 or less than 0.

Output

The output of each cases contain n lines, the rank of p1, p2… pn. Cases are separated by a single blank line.

Sample input:

1 

3 

1 1 

2 2 

3 3 

Sample output: 

0 

1 

2

Code：

    #include <iostream>
    #include <stdlib.h>

    using namespace std;

    struct Points {
        int x;
        int y;
        int rank;
    };

    struct Cases {
        int point_nums;
        Points* pointInfo;
        int* sortedArray;
    };

    int getPointX(Points* pointInfo, int index) { return pointInfo[index].x; }
    int getPointY(Points* pointInfo, int index) { return pointInfo[index].y; }

    void mergeX(Points* pointInfo, int size1, int size2, int* sortedArray) {
        int size = size1 + size2;
        int* temp = (int*)malloc(size * sizeof(int));
        int ptr1=0, ptr2=0;

        // sort x : min to max
        while ( (ptr1+ptr2) < size ) {
            if ( (ptr1 < size1 && ptr2 >= size2) || (ptr1 < size1 && getPointX(pointInfo, sortedArray[ptr1]) < getPointX(pointInfo, sortedArray[size1+ptr2])) ) {
                temp[ptr1+ptr2] = sortedArray[ptr1++];
            } else if ( (ptr2 < size2 && ptr1 >= size1) || (ptr2 < size2 && getPointX(pointInfo, sortedArray[size1+ptr2]) < getPointX(pointInfo, sortedArray[ptr1])) ) {
                temp[ptr1+ptr2] = sortedArray[size1 + ptr2++];
            } else if ( getPointX(pointInfo, sortedArray[ptr1]) == getPointX(pointInfo, sortedArray[size1+ptr2]) ) {
                if ( getPointY(pointInfo, sortedArray[ptr1]) < getPointY(pointInfo, sortedArray[size1+ptr2]) ) {
                    temp[ptr1+ptr2] = sortedArray[size1 + ptr2++];
                } else {
                    temp[ptr1+ptr2] = sortedArray[ptr1++];
                }
            }
        }
        
        for ( int i = 0 ; i < size1+size2 ; i++ ) sortedArray[i] = temp[i];

        free(temp);
    }

    void mergeYandSetRank(Points* pointInfo, int size1, int size2, int* sortedArray) {
        int size = size1 + size2;
        int* temp = (int*)malloc(size * sizeof(int));
        int ptr1=0, ptr2=0;

        // [Merge sort] sort y : max to min
        while ( ptr1+ptr2 < size1+size2 ) {
            if ( (ptr1 < size1 && ptr2 >= size2) || (ptr1 < size1 && getPointY(pointInfo, sortedArray[ptr1]) >= getPointY(pointInfo, sortedArray[size1+ptr2])) ) {
                temp[ptr1+ptr2] = sortedArray[ptr1++];
            }else if ( (ptr2 < size2 && ptr1 >= size1) || (ptr2 < size2 && getPointY(pointInfo, sortedArray[size1+ptr2]) > getPointY(pointInfo, sortedArray[ptr1])) ) {
                // set rank
                if ( ptr1+ptr2 < size1+ptr2 ) pointInfo[sortedArray[size1+ptr2]].rank += (size1+ptr2) - (ptr1+ptr2);

                temp[ptr1+ptr2] = sortedArray[size1 + ptr2++];
            }
        }

        for ( int i = 0 ; i < size1+size2; i++ ) sortedArray[i] = temp[i];

        free(temp);
    }

    void mergeSortX(Points* pointInfo, int* sortedArray, int size) {
        if ( size == 1 ) return;  

        int size1 = size / 2, size2 = size - size1;

        mergeSortX(pointInfo, sortedArray, size1);
        mergeSortX(pointInfo, sortedArray+size1, size2);
        mergeX(pointInfo, size1, size2, sortedArray);
    }

    void mergeSortYandSetRank(Points* pointInfo, int* sortedArray, int size) {
        if ( size == 1 ) return;  

        int size1 = size / 2, size2 = size - size1;

        mergeSortYandSetRank(pointInfo, sortedArray, size1);
        mergeSortYandSetRank(pointInfo, sortedArray+size1, size2);
        mergeYandSetRank(pointInfo, size1, size2, sortedArray);
    }

    void printRank(Points* pointInfo, int size) {
        for ( int i = 0 ; i < size ; i++ ) cout << pointInfo[i].rank << endl;
    }

    int main() {
        int testCase;
        Cases* cases;

        cin >> testCase;

        cases = (Cases*)malloc(testCase * sizeof(Cases));

        for ( int i = 0 ; i < testCase ; i++ ) {
            cin >> cases[i].point_nums;

            cases[i].pointInfo = (Points*)malloc(cases[i].point_nums * sizeof(Points));
            cases[i].sortedArray = (int*)malloc(cases[i].point_nums * sizeof(int));

            for ( int j = 0 ; j < cases[i].point_nums ; j++ ) {
                cin >> cases[i].pointInfo[j].x >> cases[i].pointInfo[j].y;
                cases[i].pointInfo[j].rank = 0;
                cases[i].sortedArray[j] = j;
            }
        }

        for ( int i = 0 ; i < testCase ; i++ ) {
            mergeSortX(cases[i].pointInfo, cases[i].sortedArray, cases[i].point_nums);
            mergeSortYandSetRank(cases[i].pointInfo, cases[i].sortedArray, cases[i].point_nums);

            printRank(cases[i].pointInfo, cases[i].point_nums);
            if ( i != testCase-1 ) {
                cout << endl;
            }
            free(cases[i].sortedArray);
            free(cases[i].pointInfo);
        }

        free(cases);

        system("pause");
        return 0;
    }
