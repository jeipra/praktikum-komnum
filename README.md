# Praktikum Komputasi Numerik B oleh kelompok 21

## Anggota kelompok 21:
1. Jeihan Shawmy Prasetya (5025241132)
2. Fathiya Nayla Husna Wibowo (5025241204)

## Penjelasan Kode Praktikum 2
```
def parse_function(expr):
    def f(x):
        return eval(expr)
    return f
```
eval() mengubah input menjadi fungsi yang bisa dihitung. Dengan menggunakan aturan phyton seperti diberi math. pada awal fungsi. Contoh math.exp(x) akan kembali menjadi e^x.

```
def trapezoidal(f, a, b, n):
    h = (b - a) / n
    sum = 0.5 * (f(a) + f(b))
    for i in range(1, n):
        sum += f(a + i * h)
    return sum * h
```
Mengintegrasi dengan metode trapezoidal.

```
def romberg(f, a, b, max):
    R = [[0.0 for _ in range(max)] for _ in range(max)]


    for i in range(max):
        n = 2**i
        R[i][0] = trapezoidal(f, a, b, n)


    for j in range(1, max):
        for i in range(j, max):
            R[i][j] = (4**j * R[i][j-1] - R[i-1][j-1]) / (4**j - 1)


    print("\nRomberg Integration Table:")
    for i in range(max):
        for j in range(i+1):
            print(f"{R[i][j]:.10f}", end="  ")
        print()


    print(f"\nFinal Result: {R[max-1][max-1]:.10f}")
```
Menghitung hasil integral dengan trapezoidal secara bertahap lalu mengoreksi hasil trapezoidal yang semakin besar nilainya semakin presisi.

```
if __name__ == "__main__":


    expr = input("Insert f(x): ")
    f = parse_function(expr)


    a = float(input("Lower bound a: "))
    b = float(input("Upper bound b: "))
    max = int(input("Romberg integration level (e.g. 5): "))


    romberg(f, a, b, max)
```
Menerima input user
