
## A fordítás menete
![[MobWeb ZH ábrák, pár tudnivaló 2023-11-13 13.49.11.excalidraw]]

### Manifest állomány tartalma
1. Alkalmazás komponensek listája
2. Szükséges minimális Android verzió
3. Szükséges hardware konfiguráció
4. Egyedi package név
5. Engedélyek, amelyekre az alkalmazásnak szüksége van
6. Külső API könyvtárak
## Activity lifecycle függvények
`onCreate()`: **létrejön** az activity, beállítja a megfelelő állapotokat.
`onStart()`: **láthatóvá válik** az activity, a vezérlők is. 
`onResume()`: **Fókuszt kap**ott az activity. A felhasználó eléri a vezérlőket és tudja kezelni azokat.
`onPause()`: **Másik activity kapott fókuszt**, de az activity még valamennyire láthetó a háttérben, például egy másik Activity pop-upként előjön.
`onStop()`: Az Activity **már nem látható**. Az Activity élete során többször is válthat látható/ nem látható állapot közt.
`onRestart()`: Az onStop() majd újraindítása után hívódik meg, még az indítás előtt.
`onDestroy()`: Az Activity **meg fog semmisülni.**


![[MobWeb ZH ábrák, pár tudnivaló 2023-11-13 13.47.17.excalidraw]]

## Fragment lifecycle függvények
![[MobWeb ZH ábrák, pár tudnivaló 2023-11-13 13.55.15.excalidraw]]