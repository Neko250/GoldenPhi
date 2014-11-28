---
layout: post
category: code
tags: [code, c++]
---

Here's a little C++ code I wrote that calculates the Spanish DNI Control Digits, based on information from the DNI itself (eg. name, id number, renewal date...).

#### This code is for testing purposes only!

{% highlight c++ linenos %}
#include <iostream>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#include <windows.h>
using namespace std;

int ctrlDigit(string, int&);

int main() {
    string text;
    char ans;
    int error = 0;
    
    do {
        do {
            system("cls");
            cout << "\n\tWelcome to the\n\tCtrl digit calculator.\n\t"
                 << "By Neko250; Ver. 1.0.0\n\t======================\n\n"
                 << "Type the text to calculate the ctrl digit:\n\t>>> ";
            cin >> text;

            if(ctrlDigit(text, error) == -1) {
                cout << "\nError. The text contains illegal characters:\n\t>>> "
                     << text[error] << "\n\n\tTry again !!!";
                Sleep(2000);
            }
        } while(ctrlDigit(text, error) == -1);

        cout << "\nThe Ctrl digit is:\n\t>>> " << ctrlDigit(text, error);

        do {
            cout << "\n\nDo you want to do more calculations? (y/n)\n\t>>> ";
            cin >> ans;

            if(ans != 'y' && ans != 'n') {
                cout << "\nError. Illegal answer:\n\t>>> " << ans << "\n\n\tTry again!!!";
                Sleep(2000);
                system("cls");
                cout << "\n\tWelcome to the\n\tCtrl digit calculator.\n\t"
                     << "By Neko250; Ver. 1.0.0\n\t======================\n\n"
                     << "Type the text to calculate the ctrl digit:\n\t>>> " << text
                     << "\n\nThe Ctrl digit is:\n\t>>> " << ctrlDigit(text, error);
            }
        } while(ans != 'y' && ans != 'n');
    } while(ans == 'y');

    cout << "\n\nThank you for using the program.\n";
    system("pause");
    system("cls");

    return 0;
}

int ctrlDigit(string text, int& error) {
    int m[3] = { 7, 3, 1 };
    int n = 0;

    for (int i = 0; text[i] != '\0'; i++) {
        if (isdigit(text[i])) {
            n += (text[i] - '0') * m[i % 3];
        } else if (isalpha(text[i])) {
            n += (toupper(text[i]) - 'A') * m[i % 3];
        } else {
            error = i;
            return -1;
        }
    }

    return n % 10;
}
{% endhighlight %}

---
