![[Pasted image 20241209020713.png]]
![[Pasted image 20241209020741.png]]
![[Pasted image 20241209020809.png]]
![[Pasted image 20241209020845.png]]
![[Pasted image 20241209021517.png]]

Файл:                                    Действия кода:
─────────────────────                    ─────────────────────
END_SHOW_DATA           ←── 1. fgets читает эту строку
                            2. strstr ищет "BEGIN_FIXTURE_MAPPING" - не находит
                            3. продолжаем внешний цикл while

BEGIN_FIXTURE_MAPPING   ←── 4. fgets читает эту строку
                            5. strstr находит "BEGIN_FIXTURE_MAPPING"
                            6. входим во внутренний цикл while

FIXTURE 1 27           ←── 7. fgets читает эту строку
                           8. strstr проверяет на END_FIXTURE_MAPPING - нет
                           9. sscanf извлекает числа: id=1, map=27
                           10. сохраняем: fixtureMappings[1] = 27
                           11. count++ (теперь count = 1)

FIXTURE 2 37           ←── повторяем шаги 7-11:
                           - fixtureMappings[2] = 37
                           - count = 2

FIXTURE 3 47           ←── повторяем шаги 7-11:
                           - fixtureMappings[3] = 47
                           - count = 3

FIXTURE 4 57           ←── повторяем шаги 7-11:
                           - fixtureMappings[4] = 57
                           - count = 4

END_FIXTURE_MAPPING    ←── следующий fgets читает эту строку
                           strstr находит "END_FIXTURE_MAPPING"
                           return count (возвращаем 4)
![[Pasted image 20241207224455.png]]
