# conversor-de-bases-c++
VAGNER ICILIO MACRINI 
2840482623008

#include <iostream>
#include <string>
#include <algorithm>
#include <cmath>
#include <limits>

using namespace std;

// Converte qualquer base para decimal
long long paraDecimal(string numero, int base) {

    long long resultado = 0;

    for (char caractere : numero) {

        int valor;

        if (caractere >= '0' && caractere <= '9') {
            valor = caractere - '0';
        }
        else if (caractere >= 'A' && caractere <= 'F') {
            valor = caractere - 'A' + 10;
        }
        else if (caractere >= 'a' && caractere <= 'f') {
            valor = caractere - 'a' + 10;
        }
        else {
            throw invalid_argument("Caractere invalido!");
        }

        if (valor >= base) {
            throw invalid_argument("Digito invalido para essa base!");
        }

        resultado = resultado * base + valor;
    }

    return resultado;
}

// Converte decimal para qualquer base
string deDecimal(long long numero, int base) {

    if (numero == 0) {
        return "0";
    }

    string resultado = "";
    string digitos = "0123456789ABCDEF";

    while (numero > 0) {

        int resto = numero % base;

        resultado += digitos[resto];

        numero /= base;
    }

    reverse(resultado.begin(), resultado.end());

    return resultado;
}

// Programa principal
int main() {

    int opcao;
    string numero;
    int baseOrigem, baseDestino;

    do {

        cout << "\n============================\n";
        cout << "    CONVERSOR DE BASES\n";
        cout << "============================\n";

        cout << "1 - Binario (base 2)\n";
        cout << "2 - Octal (base 8)\n";
        cout << "3 - Decimal (base 10)\n";
        cout << "4 - Hexadecimal (base 16)\n";
        cout << "5 - Sair\n";

        cout << "\nEscolha uma opcao: ";
        cin >> opcao;

        if (opcao == 5) {
            cout << "\nEncerrando programa...\n";
            break;
        }

        if (opcao < 1 || opcao > 4) {
            cout << "\nOpcao invalida!\n";
            continue;
        }

        cout << "\nDigite o numero: ";
        cin >> numero;

        cout << "\nEscolha a base de destino:\n";
        cout << "1 - Binario\n";
        cout << "2 - Octal\n";
        cout << "3 - Decimal\n";
        cout << "4 - Hexadecimal\n";

        cout << "\nOpcao: ";
        cin >> baseDestino;

        if (baseDestino < 1 || baseDestino > 4) {
            cout << "\nBase de destino invalida!\n";
            continue;
        }

        int bases[] = {0, 2, 8, 10, 16};

        baseOrigem = bases[opcao];
        baseDestino = bases[baseDestino];

        try {

            long long decimal = paraDecimal(numero, baseOrigem);

            string convertido = deDecimal(decimal, baseDestino);

            cout << "\n----------------------------\n";
            cout << "Resultado da conversao: ";
            cout << convertido << endl;
            cout << "----------------------------\n";

        }
        catch (const exception& erro) {

            cout << "\nErro: " << erro.what() << endl;

        }

    } while (true);

    return 0;
}
