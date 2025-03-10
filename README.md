# SkillForce-recruitment_task
 
# Klasteryzacja odcinków - Algorytm grupowania
Projekt przedstawia algorytm do automatycznego grupowania odcinków na obrazach w spójne „ciągłe linie”. Zastosowano podejście łączące techniki przetwarzania obrazu z klasteryzacją za pomocą DBSCAN. Projekt spełnia wymagania zarówno dla danych o wysokiej jakości ("clean"), jak i tych bardziej złożonych ("raw").

## Cel projektu
- **Identyfikacja „ciągłych linii”**: Grupowanie odcinków tak, aby wszystkie fragmenty należące do tej samej linii otrzymały wspólną etykietę.
- **Elastyczność**: Algorytm działa na uproszczonych danych („clean”) oraz na bardziej złożonych obrazach („raw”).
- **Automatyczne rozpoznanie liczby klas**: Algorytm samodzielnie określa, ile pełnych linii znajduje się na obrazie.

## Struktura danych
Dane są podzielone na następujące foldery:
- `input/raw`: obrazy o większej trudności, z szorstkimi przerywanymi odcinkami.
- `input/clean`: uproszczone wersje obrazów z wyraźniejszymi odcinkami.
- `output_gt/raw`: przykładowe wyniki dla danych raw.
- `output_gt/clean`: przykładowe wyniki dla danych clean.

Każdy z folderów zawiera obrazy na czterech poziomach trudności: `level_1`, `level_2`, `level_3`, `level_4`.

## Wymagania
- Python 3.8+.
- Biblioteki:
  - `opencv-python`
  - `numpy`
  - `scikit-learn`

Zainstaluj wymagania za pomocą polecenia:
```bash
pip install opencv-python numpy scikit-learn '''

## Jak uruchomić
1. **Skonfiguruj ścieżki wejściowe i wyjściowe**:
   - Dla danych „raw”:
     ```python
     input_dir = r"C:/path/to/input/raw"
     output_dir = r"C:/path/to/output/raw"
     ```
   - Dla danych „clean”:
     ```python
     input_dir = r"C:/path/to/input/clean"
     output_dir = r"C:/path/to/output/clean"
     ```

2. **Uruchom przetwarzanie wsadowe**:
   W skrypcie możesz wywołać funkcję `batch_process_images`:
   ```python
   batch_process_images(input_dir, output_dir, eps=50, min_samples=3)

Funkcja ta przeprocesuje wszystkie obrazy z folderu wejściowego i zapisze wyniki w folderze wyjściowym.

### Wyniki
Przetworzone obrazy zostaną zapisane w folderze wyjściowym z prefiksem `clustered_`. Przykłady:
output/raw/clustered_image1.png output/raw/clustered_image2.png


Każdy obraz wynikowy przedstawia linie oznaczone różnymi kolorami, odpowiadającymi rozpoznanym klasom.

### Dostosowanie parametrów
1. **`eps`**: Parametr algorytmu DBSCAN określający promień klasteryzacji.
   - Wyższe wartości `eps` zwiększają zakres grupowania odcinków, co może być pomocne w przypadku bardziej rozdzielonych fragmentów.
   - Przykład: na danych „raw” może być konieczne zwiększenie `eps`, aby poprawnie grupować zniekształcone odcinki.
2. **`min_samples`**: Minimalna liczba punktów wymagana do utworzenia klastra.
   - Niższe wartości są odpowiednie dla danych „clean”, gdzie odcinki są bardziej spójne.
   - Wyższe wartości mogą lepiej filtrować szum w danych „raw”.

### Testowanie
1. **Uruchamianie algorytmu na danych „clean”**:
   - Ustaw ścieżki `input_dir` i `output_dir` dla danych „clean” w skrypcie:
     ```python
     input_dir = r"path/to/input/clean"
     output_dir = r"path/to/output/clean"
     batch_process_images(input_dir, output_dir, eps=30, min_samples=2)
     ```
   - Algorytm automatycznie przetworzy obrazy na poziomach trudności `level_1` do `level_4` i zapisze wyniki w folderze `output/clean`.

2. **Uruchamianie algorytmu na danych „raw”**:
   - Ustaw ścieżki `input_dir` i `output_dir` dla danych „raw” w skrypcie:
     ```python
     input_dir = r"path/to/input/raw"
     output_dir = r"path/to/output/raw"
     batch_process_images(input_dir, output_dir, eps=50, min_samples=3)
     ```
   - W razie potrzeby dostosuj parametry `eps` i `min_samples`, aby uzyskać lepsze wyniki.

3. **Przegląd wyników**:
   - Przejrzyj zapisane obrazy w folderze wyjściowym, aby ocenić skuteczność klasteryzacji.
   - Wyniki powinny pokazywać prawidłowo pogrupowane odcinki z odpowiednim kolorowaniem.


