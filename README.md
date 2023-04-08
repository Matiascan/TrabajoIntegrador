# TrabajoIntegrador
using namespace std;

// Estructura para almacenar la información de un participante
struct Participante {
    string nombre;
    int puntos = 0;
};

int main() {
    // Mapa para almacenar los participantes por nombre
    map<string, Participante> participantes {
        {"argentina", {"Argentina"}},
        {"mexico", {"México"}},
        {"polonia", {"Polonia"}},
        {"arabia saudita", {"Arabia Saudita"}}
    };

    // Vector para almacenar la información de los resultados de los partidos
    vector<pair<string, string>> resultados {
        {"argentina", "mexico"},
        {"polonia", "arabia saudita"},
        {"argentina", "polonia"},
        {"mexico", "arabia saudita"},
        {"argentina", "arabia saudita"},
        {"mexico", "polonia"}
    };

    // Vector para almacenar la información de los pronósticos
    vector<pair<string, string>> pronosticos {
        {"argentina", "mexico"},
        {"polonia", "arabia saudita"},
        {"argentina", "polonia"},
        {"mexico", "arabia saudita"},
        {"argentina", "arabia saudita"},
        {"mexico", "polonia"}
    };

    // Calcular los puntos de los participantes según los resultados y pronósticos
    for (auto& resultado : resultados) {
        string equipo1 = resultado.first;
        string equipo2 = resultado.second;

        int puntos_equipo1 = 0;
        int puntos_equipo2 = 0;

        for (auto& pronostico : pronosticos) {
            string pronostico_equipo1 = pronostico.first;
            string pronostico_equipo2 = pronostico.second;

            if (pronostico_equipo1 == equipo1 && pronostico_equipo2 == equipo2) {
                puntos_equipo1 += 3;
            } else if (pronostico_equipo1 == equipo2 && pronostico_equipo2 == equipo1) {
                puntos_equipo2 += 3;
            } else if (pronostico_equipo1 == equipo1 || pronostico_equipo2 == equipo1) {
                puntos_equipo1 += 1;
            } else if (pronostico_equipo1 == equipo2 || pronostico_equipo2 == equipo2) {
                puntos_equipo2 += 1;
            }
        }

        participantes[equipo1].puntos += puntos_equipo1;
        participantes[equipo2].puntos += puntos_equipo2;
    }

    // Ordenar los participantes por puntaje descendente
    vector<Participante> ranking;
    transform(participantes.begin(), participantes.end(), back_inserter(ranking),
        [](const pair<string, Participante>& p) { return p.second; });
    sort(ranking.begin(), ranking.end(),
        [](const Participante& p1, const Participante& p2) { return p1.puntos > p2.puntos; });

    // Imprimir el ranking
    cout << "Ranking:\n";
    for (int i
