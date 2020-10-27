# Shortest-unique-prefix
Given a list of words, return the shortest unique prefix of each word. For example, given the list:      dog     cat     apple     apricot     fish  Return the list:      d     c     app     apr     f



#include <bits/stdc++.h>
using namespace std;
 
vector<string> uniquePrefix(vector<string> &a)
{
    int size = a.size();
 
    /* create an array to store the results */
    vector<string> res(size);
 
    /* sort the array of strings */
    sort(a.begin(), a.end());
 
    /* compare the first string with its only right 
    neighbor */
    int j = 0;
    while (j < min(a[0].length() - 1, a[1].length() - 1))
    {
        if (a[0][j] == a[1][j])
            j++;
        else
            break;
    }
    int ind = 0;
    res[ind++] = a[0].substr(0, j + 1);
 
    /* Store the unique prefix of a[1] from its left neighbor */
    string temp_prefix = a[1].substr(0, j + 1);
    for (int i = 1; i < size - 1; i++)
    {
        /* compute common prefix of a[i] unique from 
        its right neighbor */
        j = 0;
        while (j < min(a[i].length() - 1, a[i + 1].length() - 1))
        {
            if (a[i][j] == a[i + 1][j])
                j++;
            else
                break;
        }
 
        string new_prefix = a[i].substr(0, j + 1);
 
        /* compare the new prefix with previous prefix */
        if (temp_prefix.length() > new_prefix.length())
            res[ind++] = temp_prefix;
        else
            res[ind++] = new_prefix;
 
        /* store the prefix of a[i+1] unique from its 
        left neighbour */
        temp_prefix = a[i + 1].substr(0, j + 1);
    }
 
    /* compute the unique prefix for the last string 
    in sorted array */
    j = 0;
    string sec_last = a[size - 2];
 
    string last = a[size - 1];
 
    while (j < min(sec_last.length() - 1, last.length() - 1))
    {
        if (sec_last[j] == last[j])
            j++;
        else
            break;
    }
 
    res[ind] = last.substr(0, j + 1);
    return res;
}
 
// Driver Code
int main()
{
    vector<string> input = {"dog", "cat", "apple", "apricot", "fish"};
    vector<string> output = uniquePrefix(input);
    cout << "The shortest unique prefixes in sorted order are : \n";
 
    for (auto i : output)
        cout << i << ' ';
 
    return 0;
}
