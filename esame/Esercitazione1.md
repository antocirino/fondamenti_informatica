# Esercitazione 1
main.cpp
```c++
#include <iostream>
#include <fstream>
#include <string.h>
using namespace std;

#define maxdim 100

struct bracci_robot {
    char identificativo[6];
    double velocita;
    double temperatura;
};

typedef bracci_robot robot;

int caricaFile (robot [], int &);
void stampa (robot [], int);
double massimo (robot [], int);
void maiuscolo (robot [], int, double);
void cancellazione (robot[], int &);

int main() {
    int riemp;
    robot vettore[maxdim];
    int pos;
    double maxTemp;
    
    if (caricaFile(vettore, riemp)==1) {
        cout << "Errore! File mancante.";
        return 0;
    }
    
    cout << "Elenco bracci robotici: " << endl;
    stampa(vettore, riemp);
    
    maxTemp = massimo (vettore, riemp);
    maiuscolo(vettore, riemp, maxTemp);
    cout << "Evidenziando il primo carattere dei bracci robot a temperatura più alta: " << endl;
    stampa (vettore, riemp);
    
    cout << "Cancellando i bracci robotici con identificativo che inizia con una lettera compresa tra a e d:" << endl;
    cancellazione (vettore, riemp);
    stampa (vettore, riemp);
    
    return 0;
}

int caricaFile (robot vettore[], int &riemp) {
    fstream mioFile;
    mioFile.open("robot.txt", ios::in);
    if (!mioFile) {
        return 1;
    } else {
        mioFile >> riemp;
        
        for (int i=0; i<riemp; i++) {
            mioFile >> vettore[i].identificativo;
            mioFile>> vettore[i].velocita;
            mioFile >> vettore[i].temperatura;
        }
        mioFile.close();
        return 0;
    }
}

void stampa (robot vettore[], int riemp) {
    for (int i=0; i<riemp; i++) {
        cout << "(" << vettore[i].identificativo << ", " << vettore[i].velocita << ", " << vettore[i].temperatura << ")" << endl;
    }
    
}

double massimo (robot vettore[], int riemp) {
    double massimoTemperatura = vettore[0].temperatura;
    for (int i=0; i<riemp; i++) {
        if (vettore[i].temperatura > massimoTemperatura) {
            massimoTemperatura = vettore[i].temperatura;
        }
    }
    return massimoTemperatura;
}

void maiuscolo (robot vettore[], int riemp, double max) {
    for (int i=0; i<riemp; i++) {
        if (vettore[i].temperatura == max){
            vettore[i].identificativo[0] = toupper(vettore[i].identificativo[0]);            
        }
    }
}

void cancellazione (robot vettore[], int &riemp) {
    for (int i=0; i<riemp; i++) {
        if (vettore[i].identificativo[0]>='a' && vettore[i].identificativo[0]<='d') {
            for (int j=i; j<riemp-1; j++) {
                vettore[j] = vettore[j+1];
            }
            riemp--;
            i--;
        }
    }
}
```

robot.txt
```
12
afhop
12
20.4
bbtro
1.3
6.8
ccgui
13.9
30.8
mrnlm
12.7
31.5
drefg
3.6
25.2
plimr
10.9
12.4
crhiu
6.4
26.2
racpo
16.4
19.8
brumm
17.4
11.8
cruck
19.4
1.8
zebra
8.4
12.3
oprpi
12.7
31.5
```
