import tkinter as tk
from tkinter import messagebox
import random

class Participant:
    def __init__(self, name, country):
        self.name = name
        self.country = country

class Event:
    def __init__(self, name):
        self.name = name
        self.participants = []
        self.results = []

    def add_participant(self, participant):
        self.participants.append(participant)

    def simulate_event(self):
        if len(self.participants) < 3:
            messagebox.showerror("Error", "Necesitas al menos 3 participantes para simular este evento.")
            return

        self.results = random.sample(self.participants, 3)
        return self.results

class OlympicGames:
    def __init__(self):
        self.events = []
        self.participants = []
        self.medal_tally = {}

    def add_event(self, event_name):
        event = Event(event_name)
        self.events.append(event)

    def add_participant(self, name, country):
        participant = Participant(name, country)
        self.participants.append(participant)

    def assign_participants_to_event(self, event_name):
        event = next((event for event in self.events if event.name == event_name), None)
        if event:
            for participant in self.participants:
                event.add_participant(participant)

    def simulate_event(self, event_name):
        event = next((event for event in self.events if event.name == event_name), None)
        if event:
            results = event.simulate_event()
            if results:
                self.update_medal_tally(results)
                return results
        return None

    def update_medal_tally(self, results):
        medals = ['Oro', 'Plata', 'Bronce']
        for i, participant in enumerate(results):
            country = participant.country
            if country not in self.medal_tally:
                self.medal_tally[country] = {'Oro': 0, 'Plata': 0, 'Bronce': 0}
            self.medal_tally[country][medals[i]] += 1

    def show_medal_tally(self):
        return self.medal_tally


class OlympicsApp:
    def __init__(self, root):
        self.games = OlympicGames()

        root.title("Simulador Juegos Olímpicos")

        # Labels y Entry para registrar eventos
        self.event_label = tk.Label(root, text="Registrar Evento:")
        self.event_label.pack()
        self.event_entry = tk.Entry(root)
        self.event_entry.pack()
        self.add_event_button = tk.Button(root, text="Agregar Evento", command=self.add_event)
        self.add_event_button.pack()

        # Labels y Entry para registrar participantes
        self.participant_label = tk.Label(root, text="Registrar Participante (Nombre, País):")
        self.participant_label.pack()
        self.participant_name_entry = tk.Entry(root)
        self.participant_name_entry.pack()
        self.participant_country_entry = tk.Entry(root)
        self.participant_country_entry.pack()
        self.add_participant_button = tk.Button(root, text="Agregar Participante", command=self.add_participant)
        self.add_participant_button.pack()

        # Botón para asignar participantes a eventos
        self.assign_button = tk.Button(root, text="Asignar Participantes a Evento", command=self.assign_participants)
        self.assign_button.pack()

        # Labels y Entry para simular eventos
        self.simulate_label = tk.Label(root, text="Simular Evento:")
        self.simulate_label.pack()
        self.simulate_event_entry = tk.Entry(root)
        self.simulate_event_entry.pack()
        self.simulate_button = tk.Button(root, text="Simular", command=self.simulate_event)
        self.simulate_button.pack()

        # Botón para mostrar la tabla de medallas
        self.show_medal_tally_button = tk.Button(root, text="Mostrar Tabla de Medallas", command=self.show_medal_tally)
        self.show_medal_tally_button.pack()

        # Área de resultados
        self.results_text = tk.Text(root, height=10, width=50)
        self.results_text.pack()

    def add_event(self):
        event_name = self.event_entry.get()
        if event_name:
            self.games.add_event(event_name)
            messagebox.showinfo("Evento añadido", f"Evento '{event_name}' añadido.")
        else:
            messagebox.showerror("Error", "Debes ingresar un nombre de evento.")

    def add_participant(self):
        name = self.participant_name_entry.get()
        country = self.participant_country_entry.get()
        if name and country:
            self.games.add_participant(name, country)
            messagebox.showinfo("Participante añadido", f"Participante '{name}' de {country} añadido.")
        else:
            messagebox.showerror("Error", "Debes ingresar el nombre y el país del participante.")

    def assign_participants(self):
        event_name = self.event_entry.get()
        if event_name:
            self.games.assign_participants_to_event(event_name)
            messagebox.showinfo("Asignación completada", f"Participantes asignados al evento '{event_name}'.")
        else:
            messagebox.showerror("Error", "Debes ingresar el nombre del evento.")

    def simulate_event(self):
        event_name = self.simulate_event_entry.get()
        if event_name:
            results = self.games.simulate_event(event_name)
            if results:
                self.results_text.delete(1.0, tk.END)
                self.results_text.insert(tk.END, f"Resultados del evento '{event_name}':\n")
                self.results_text.insert(tk.END, f"Oro: {results[0].name} ({results[0].country})\n")
                self.results_text.insert(tk.END, f"Plata: {results[1].name} ({results[1].country})\n")
                self.results_text.insert(tk.END, f"Bronce: {results[2].name} ({results[2].country})\n")
            else:
                messagebox.showerror("Error", "El evento no tiene suficientes participantes.")
        else:
            messagebox.showerror("Error", "Debes ingresar el nombre del evento.")

    def show_medal_tally(self):
        medal_tally = self.games.show_medal_tally()
        if medal_tally:
            self.results_text.delete(1.0, tk.END)
            self.results_text.insert(tk.END, "Tabla de Medallas:\n")
            for country, tally in sorted(medal_tally.items(), key=lambda x: (-x[1]['Oro'], -x[1]['Plata'], -x[1]['Bronce'])):
                self.results_text.insert(tk.END, f"{country}: Oro {tally['Oro']}, Plata {tally['Plata']}, Bronce {tally['Bronce']}\n")
        else:
            self.results_text.delete(1.0, tk.END)
            self.results_text.insert(tk.END, "No hay medallas asignadas aún.\n")


# Ejecutar la aplicación
if __name__ == "__main__":
    root = tk.Tk()
    app = OlympicsApp(root)
    root.mainloop()
