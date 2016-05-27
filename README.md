Код был написан для текста "Записок о Галльской войне", представленном на сайте thelatinlibrary.com. На текстах другого формата программа не будет работать. Язык программирования - Python 3.3.
Текст каждой книги был скопирован, сохранен в формате txt и помещен в одну папку с программой.
Программа работает для одной книги произведения. То есть, чтобы запустить ее для отдельной книги, необходимо видоизменить код, а именно название файла, который открывает программа (т.е. изменить номер книги).
Программа не идеальна, и, к сожалению, не находит вхождения с предлогом с большой буквы, т.е. вхождения в начале предложения (их нужно искать вручную). 
На экран сначала массивом выводится схематичное распределение вхождений по книгам. Символ [ ] обозначает одну пронумерованную группу предложений (в виде таких секций представлен текст "Записок...", представленных на веб-сайте. Чаще это два-три предложения). Группа секций - это абзац, абзацы в схеме также пронумерованы. Далее массивом выводятся сначала все вхождения с предлогом. До и после массива представлено число - количество всех вхождений с предлогом.
Автоматически к каждому вхождению приписывается адресация: номер книги, номер абзаца, номер секции. Каждый раз призапуске программы для новой книги нужно изменять название файла, для которого работает программа, а также номер книги, который будет приписываться каждому вхождению.

В конце работы программа создает csv-файл с результатами (а именно списком вхождений). 

Код программы простой, т.е. не предназначен для сложной автоматической обработки полученных результатов, а также не прездназначен для текстов разного формата, так как программа была написана в рамках узкого исследования, где способ выявления всех вхождений с предлогом в сочинении Цезаря "Записки о Галльской войне" не имеет большого значения.





    import re
    f=open('книга I.txt', 'r', encoding='utf-8')    #Открытие файла. Изменить название файла призапуске кода для другой книги
    fw=open('книга I.csv', 'w', encoding='utf-8')   #Создание csv-файла. Изменить название файла призапуске кода для другой книги
    s=f.read()  
    e=re.split('\[[0-9]*\]', s) #разделение файла на пронумерованные секции (2-3 предложения) согласно формату текста
    p=1
    n=0
    v=[]
    u=1
    pp=[]
    for y in e:
        ll=0
        if y==e[0]:
            continue
        else:
            print(p)
            z=re.split(' [0-9]* ', y)    #разделение секций на предложение
            for i in z:
                pp.append(u)
                u+=1
            for l in z:
                q=re.findall(' (?:A|a)b? [A-Za-z]*', l)
                if l==z[0]:
                    continue
                else:
                    print(q)
                    for t in q:
                        v.append(t+' '+'1'+' ' +str(p)+' '+str(pp[ll])) #приписывание адресации к вхождению. 1-номер книги. 
                        n+=1
                ll+=1
            p+=1
    print(n)
    print(v)
    print(len(v))
    for b in v:
            o=re.search('ab [jyaeiuohAEIUOHYJ]', b)   #поиск вхождений алломорфа 'а' с лексемами на гласный или придыхательный [h]
            if o:
                fw.write(b + ';'+'ab v' + '\n')          #запись данных в csv-файл
            y=re.search('ab [bcdfgklmnpqrstvwxzBCDFGKLMNPQRSTVWXZ]', b)        #поиск вхождений алломорфа с лексемами на согласный 
            if y:
                fw.write(b + ';'+'ab c'+ '\n')          #запись данных в csv-файл
            rr=re.search('a [jyaeiuohAEIUOHYJ]', b)             #поиск вхождений алломорфа 'ab' с лексемами на гласный и [h]
            if rr:
                fw.write(b + ';'+ 'a v'+ '\n')          #запись данных в csv-файл
            yy=re.search('a [bcdfgklmnpqrstvwxzBCDFGKLMNPQRSTVWXZ]',b)  #поиск вхождений алломорфа с лексемами на согласный
            if yy:
                fw.write(b + ';'+'a c'+ '\n')             #запись данных в csv-файл
    f.close()
    fw.close()

