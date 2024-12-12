from abc import ABC, abstractmethod

# Definimos la interfaz
class IConversionTemperatura(ABC):
    @abstractmethod
    def convertirTemperaturas(self, temperaturaCelsius):
        """Convierte una temperatura en grados Celsius a Fahrenheit y Kelvin."""
        pass
    
    @abstractmethod
    def verificarCongelacionEBullicion(self):
        """Verifica si la temperatura está en los puntos de congelación o ebullición."""
        pass


# Implementamos la clase concreta que hereda de la interfaz
class ConversionTemperatura(IConversionTemperatura):
    # Atributos: Encapsulación
    def __init__(self):
        self.__temperaturaCelsius = 0.0
        self.__temperaturaFahrenheit = 0.0
        self.__temperaturaKelvin = 0.0

    # Métodos: Cada uno resuelve un caso de uso
    def setTemperaturaCelsius(self, temperaturaCelsius):
        """Establece la temperatura en grados Celsius y actualiza las conversiones."""
        self.__temperaturaCelsius = temperaturaCelsius
        self.__temperaturaFahrenheit = (self.__temperaturaCelsius * 9/5) + 32
        self.__temperaturaKelvin = self.__temperaturaCelsius + 273.15

    def getTemperaturaCelsius(self):
        """Obtiene la temperatura en grados Celsius."""
        return self.__temperaturaCelsius

    def getTemperaturaFahrenheit(self):
        """Obtiene la temperatura en grados Fahrenheit."""
        return self.__temperaturaFahrenheit

    def getTemperaturaKelvin(self):
        """Obtiene la temperatura en grados Kelvin."""
        return self.__temperaturaKelvin

    def convertirTemperaturas(self, temperaturaCelsius):
        """Convierte la temperatura de grados Celsius a Fahrenheit y Kelvin."""
        # Precondición: Se recibe una temperatura en grados Celsius
        self.setTemperaturaCelsius(temperaturaCelsius)
        # Postcondición: Temperaturas convertidas a Fahrenheit y Kelvin
        return self.__temperaturaFahrenheit, self.__temperaturaKelvin

    def verificarCongelacionEBullicion(self):
        """Verifica si la temperatura corresponde al punto de congelación o ebullición en alguna escala."""
        if self.__temperaturaCelsius == 0:
            estado = "Congelación del agua (Celsius)"
        elif self.__temperaturaCelsius == 100:
            estado = "Ebullición del agua (Celsius)"
        elif self.__temperaturaFahrenheit == 32:
            estado = "Congelación del agua (Fahrenheit)"
        elif self.__temperaturaFahrenheit == 212:
            estado = "Ebullición del agua (Fahrenheit)"
        elif self.__temperaturaKelvin == 273.15:
            estado = "Congelación del agua (Kelvin)"
        elif self.__temperaturaKelvin == 373.15:
            estado = "Ebullición del agua (Kelvin)"
        else:
            estado = "No corresponde al punto de congelación o ebullición en ninguna escala"
        
        # Postcondición: Devuelve el estado de la temperatura en relación a la congelación o ebullición
        return estado
