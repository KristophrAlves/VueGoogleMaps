<template>
  <div class="container" id="map"></div>
</template>

<script>
export default {
  name: "MapComponent",
  mounted() {
    this.initMap();
  },
  methods: {
    async initMap() {
      const positions = [
        { lat: -15.788221568796175, lng: -47.8817336566898, icon: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAACXBIWXMAAAsTAAALEwEAmpwYAAACYklEQVR4nO2YPWtUQRSGHxRR1BQGFONXYaHRxmhQE/EvaCUWtkIstF7ttLeRxPgHUljlgwh2gpWC9nZipRYibqKQrBFfmXAWLsvee+feu+6dXaY4xc6cmXeee86Zj0WgYTDqXkAEIUaE2tNHsUao/0srRoT6v65iRKj/i8aIMGxXlJ+gO6BR96MPdgA0A/rVa5CZPgF02t1eg4zaxO/7lAJvTe9gr0Gwifuaz/9BkwhCjIiGLrUOe+xuh0A3QR9CBili+0CroYIsePh+BF03/z2gNyGC+Pr/Ad22MSdA30MHaYEaoLGcNLsG+hsySKNAzTwOGeSItb/IGPsStAO0q6NeggLBcy0PzO846Nsgg2yBrprvjUEGEegTaLf5vx5kECW25FuhgRyz9uee87wy/5OhgTwseX3ZGRrIlsG0I1PQwgFRhbkiiGJEqC+1NkBPQBdBe80ugWZBmz2skY0OHfeYmgLN2c24Eshn0LmM3WIC9KUHIHk6582nFMhmYvKzoBXQutkyaDwh0qoA4qtzoYuOF8is9Z0BNbv0NxMi8xVAiug8TQMZy3g/T1vfSsailszniifEu4T4agmdqUTbgrVtv2N8XmXrGQJrJa8VZXVGuozbfp+4/GwkXmdFBZoFF+v+NL8HegQ6WkJnJOHv1nzf6sa1pA5uh3w5w2exYGpV1ZlOq7ssgTkbPJ5ShD9Ap8znWQWQIjrzZUBadk64CU5bwa2ZLSYm77YtFjFfnUnQ7zIgskNoIueg+loBwldnMufgzQVx5jYEF/7Ldm1oXx3cnl4lEnk6+632XDqlRaIN8g/x86ZpwPmtXAAAAABJRU5ErkJggg==' },
        { lat: -15.654163903776386, lng: -47.76088317271795, icon: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAACXBIWXMAAAsTAAALEwEAmpwYAAAClElEQVR4nO1ZTW/TQBCdxEmdNmnSxpA0oU28agP39gASJ1SJngoHuCEh4Io4UIS4IA4IblzaA0ggPtQW/DMHTcdW3cgfu3YSb6I9jBTtjvz2zZsZ7zgAnsCFMCj6AIaIMIpg4enjmRoRxUfaM4qI4qPrGUVE8RE1iggOwuIo8nuIsL+K0CgjAEzf6mXG++NOmMj+6mwIjNv95oSJNHwlPvdnkwIf+4zXtCZMBPwIzTSfp4AJhogwisDCpdaald7dmhbCnTrCl02NiaiYXUJ429WUyMvr6b7HWwh7K+xfLXH71o6IrP9fgXDPf3FfqyD8GGpO5MxFOGyl187uCsI/nYkctuRr5klbYyLrvhJJRf1uA6EECNZYvWhFBCTP8nCN/ZwKwvfBHBM5dxFu1dj3dn2OiXgC4WSL2zH5f+jNMREv1JLvNjQj0q7w+quO3HPeb7B/p6IZkUd+EataGTQjcu4ymUAZNdOIiJfjWYaIZxTB4lLr1EV46iBs2zzgkNHvZw7vTapGTiNwRj4O3YxzEfk6QBguxXcL2vs2yE8kDcddYp9MRChCwcM3qwhvugi/hmz0u1+9BImLmAwRWRwRgSNFhCSlvRtVhJ8RUxmtBSAvnOxEVHCeOzFEgmksan6m/KQ9ikrcoY667HOzJkfik//JNDx3qOCM7Ms1OjOtXcwxMlMZSRwHQHtZrhVZcZYj/jW4mE8oP4lMMJ2pApDsKoelj+YHTYTH6whtSx1nOUSEzvygxXWTmAYykr/uqKVWXpxRKLWu1EoSQFCE/YQi7GUo9mngQBLAWagtEshRqC1ShHoJbVHFpHFsviErE5F9Uam+ELPgCDsZRwqEGgLJvzN2daCenkeJNJxamWuP0ilOCd/+Aw9+8PyCJuMSAAAAAElFTkSuQmCC' },
        { lat: -16.694349814572508, lng: -49.24030225475105, icon: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAACXBIWXMAAAsTAAALEwEAmpwYAAAC80lEQVR4nO2Zy2sTURTGP1pKSxvBiNU+BYU+FLSNsUla/AsUBVG6cCO00Aq6qUIVXejKha8Wte4EQbCKj4pCceMDBQUFV9KVVRBtrRLb1A4+Kn5yejtEm0wyM0mTSZjF2dw59373d885d+6dgUYwHwzZnoALQjciyHr6aG6NMPsrrbkRYfZXV3MjwuyvqBsR5tsRZeIb2NkNepeBwOLbUi/Y0QV+nkkzSEdXZgAWWve+NIN45yPx9GVmUuDRc6W3vDzNIJhfoYzm8yJowgWhGxHmXWqtrEi+u5WvAHe2g69GHAxixcrKwBt3HQpy6Upy39ej4Nbtyr+kBHz4zIEgZv2nf4N7OlWf2lXgh7DDQSZ/gj29YEVl4jTbsg2c+eNgkJ5e8zVz4pSDQSqrVPvNe8Z9h4bBggKwqOj/enEUCEzO5eBh5VdTC77/ksMgkVmwbbPy3bErh0E0giPvwOJi5X//cQ6DaIxuye27HQZSXaPaLw+aG2f4gfJfvcZhIEeO2Tu+FBY6DCQyq2D0yFg054BoKYzlgmhuRJC91Ap/B0/2g/4WsLRU2aYAePoc+PVH+mokvEBHLlOBEHjmvDoZpwTy5iO4vsl4t9jQDI6OpQ6STKfJp3xsgchq64M3rgOv3wEnppVdGwLrG6MiRitmBsSsTvPGWB1TIJI68qxhLTg+Fftc2nSRvgH7IFZ0zl4wANFvY/Huz8FW9UxWyGhSg7eVT6jNHMSTF1Fx/WOCFZ1AKNomc5a2uXuMmVuZhNhI4FPE3rHCro5nSWy/ufuJ5KfA6LczqwISdiuTlY/me/eDR4+DVdXWdTz/gMicDxxSdZPwR48ecik4I5+rt6ylVqo6wVaDukskIPu3dJZCi1eEY5NgXb3y6b9oH8SKTt+ADRAJmbwnZIC6BlVwkqtiskL64PG2RStmVsfnB6d+2QARk5eQLmL0ono7bh/CrI7Pn/jFa+pnqGwIEv6WoDo26EcH2dNTiUQyHY9H1Z6kk1EkdJC/5W5CjiekD5kAAAAASUVORK5CYII=' },
        { lat: -16.303969121710093, lng: -47.24897716966462, icon: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAACXBIWXMAAAsTAAALEwEAmpwYAAADM0lEQVR4nO2Zy08TURSHp5RC7bQWKG1pUYxgaMFIecRCi4mxWDSKUKKioSiPOigBeTlBd7p3YxT8B1y4Uowm7kxcaaJ7d8aVujDGZ+ID4zHnpNOo7bQz09JOySzO5s6593e/e865c+8Mw3MAG8GYQk9AA+G0iEDB04fXaoQr/ErzWkS4wq8ur0WEK/yKahHhNtoRZW7sC/iazoKxvAoYhll3M5ZXQot3EubGv+YWpMU7mReA/62teTq3IMZ4JEYiz/OSAtGBp6RnMtpzC8LEVyiv+bwOmowGwmkRgQ2XWqypJuPuZtrkAE/9EIwff6FeEDlmKGVhsPe+OkEO7buV0Zc7+RIatvWTf6neCMP9T9QHItX/wplfsMsToz6bzXUwc/q9ukEWYj/A71sC1uRKm2YNdUeA536rF8TvW5JcM3s7r6oXxGxyU/vggQeifY8efAg6XQmUlBj+qRdVgTAS59LZeon8LOxWmD71rnhBFmNrUFuzh3wbtx8rXhCetuVXoNeXk/+JvsfFC8JzkNiSm3YMqwvEwm6h9r7QbUnjDB1+RP5WS726QILtlxUdX3Q6vbpAFmNrBCNERqapB4TPYiwNhNciAoVLrfmJbxAKXIMa+24wlJrIXHY/hILXYWHie85qZD5JhwWXowt6gjfoZJwVyLnoa7DbfKK7hcPWClPRN1mDZNZpIx9FILjawuC2ymaI9N6D2bHPZJHwKlRVeBMiYismBUSqjrO6PUlHEgimDg1e0QTnRz8mPcc2QWR/94piEDk6Pd3LqUGE21iq+7PbGaBnuEJikxoI3yUftzMoCWIk8iwhLnxMkKPjcnQl2nDO2Eb3GCm3MgyxmMDs6CdFxwqlOmUGS1I/up9gfiKMcDuTK4BhlzNZ/GjetnMGgh1XwMzWytYp+wsE5+z3XaS6SfujJxHy8GqakN+RlVrZ6wRS1106Ady/sTMWWuoi/ACV1sZ4sd9UDCJPZ0U+CIYM3xMkYvVQwWGuouEKCYOn2hblmHSdDliM/ZQPgoYvIUFE7EU1FX2rGEKqjrO6I+2LV9LPUNwQMPwuRycdGxJHh+7lrCKRUcdgptrDdBKLhADyB1R+Y+jBuDrbAAAAAElFTkSuQmCC' }
      ];

      try {
        const map = new google.maps.Map(document.getElementById("map"), {
          mapId: "DEMO_MAP_ID",
        });

        const bounds = new google.maps.LatLngBounds();

        positions.forEach(position => {
          const marker = new google.maps.Marker({
            position: position,
            map: map,
            title: "Marcador",
            icon: {
              url: position.icon,
              scaledSize: new google.maps.Size(40, 40),
            }
          });
          bounds.extend(position);

          marker.addListener('click', () => {
            const infoWindow = new google.maps.InfoWindow({
              content: `Latitude: ${position.lat}, Longitude: ${position.lng}`,
            });
            infoWindow.open(map, marker);
          });
        });

        map.fitBounds(bounds);
      } catch (error) {
        console.error("Erro ao carregar a API do Google Maps:", error);
      }
    },
  },
};
</script>

<style scoped>
.container {
  width: 100%;
  height: 100vh;
}
</style>
