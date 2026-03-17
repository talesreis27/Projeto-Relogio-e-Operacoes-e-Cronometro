[projeto_relogio.py](https://github.com/user-attachments/files/26048848/projeto_relogio.py)
import time


class Relogio:

    def __init__(self, horas: int, minutos: int, segundos: int):
        self.horas = horas %24
        self.minutos = minutos %60
        self.segundos = segundos %60

    def __str__(self):
        return f"{self.horas:02d}:{self.minutos:02d}:{self.segundos:02d}"

    def __repr__(self):
        return f"Relogio({self.horas}, {self.minutos}, {self.segundos})"

    def _para_segundos(self):
        return self.horas * 3600 + self.minutos * 60 + self.segundos

    @staticmethod
    def _para_horas(total):
        total = total %86400
        h = total // 3600
        m = (total % 3600) // 60
        s = total % 60
        return Relogio(h, m, s)

    #DEFS ARITIMETICOS

    def __add__(self, other:'Relogio'):
        return Relogio._para_horas(self._para_segundos() + other._para_segundos())

    def __sub__(self, other: 'Relogio'):
        diff =  abs(self._para_segundos() - other._para_segundos())
        return self._para_horas(diff)
    #DEFS BOOLS

    def __eq__(self, other):
        return self._para_segundos() == other._para_segundos()

    def __ne__ (self, other):
        return self._para_segundos() != other._para_segundos()

    def __gt__(self, other):
        return self._para_segundos() > other._para_segundos()

    def __lt__(self, other):
        return self._para_segundos() < other._para_segundos()

    def __ge__(self, other):
        return self._para_segundos() >= other._para_segundos()

    def __le__(self, other):
        return self._para_segundos() <= other._para_segundos()


    class Cronometro:
        """"
        class Cronometro:
            __init__ > Devine os objetos da class
            start > iniciar o cronometro
            pause > pausa o cronometro
            restart >  zera e recincia o cronometro
            stop > para o cronometro e retorna o cronometro e devolve o valor na qual o mesmo parou
            show_time > mostra o valor em que o cronometro parou
            __str__ >  mostra todos o valor do cronumetro em formato de relogio"""
        def __init__(self):
            self._inicio = None
            self._pausado = 0.0
            self._a_correr = False

        def start(self):
            if not self._a_correr:
                self._inicio = time.time() - self._pausado
                self._a_correr = True
                print(f"Cronometro INICIADO")

        def pause(self):
            if self._a_correr:
                self._pausado = time.time() - self._inicio
                self._a_correr = False
                print(f"Cronometro PAUSADO em {self._pausado:.2f} segundos")

        def restart(self):
            self._inicio = time.time()
            self._pausado = 0.0
            self._a_correr = True
            print(f"Cronometro RENINCIADO")

        def stop(self):
            if self._a_correr:
                self._pausado= time.time() - self._inicio
                self._a_correr = False
            total = self._pausado
            print(f"Cronometro PARADO. Tempo Total: {total:.2f} segundos")
            return total

        def show_time(self):
            if self._a_correr:
                return time.time() - self._inicio
            else:
                return self._pausado

        def __str__(self):
            t = self.show_time()
            h = int(t//3600)
            m = (t % 3600) // 60
            s = t % 60
            return f"{h:02d}:{m:02d}:{s:02d}"


if __name__ == "__main__":

        r1 = Relogio(horas=4, minutos=20, segundos=0)
        print(r1)
        r2 = Relogio(horas=16, minutos=30, segundos=30)
        print(r2)
        print(r1 + r2)
        print(r1 - r2)
        print(r1 > r2)
        print(r1 < r2)
        print(r1 >= r2)
        print(r1 <= r2)


        c1 = Relogio.Cronometro()
        c1.start()
        time.sleep(0.5)
        c1.pause()
        c1.start()
        time.sleep(0.5)
        c1.stop()
        c1.restart()
        time.sleep(0.5)
        c1.stop()
        c1.restart()
        print(f"{c1.show_time():.2f}")
