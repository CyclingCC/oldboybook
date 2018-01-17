#### grep

\[root@oldboy36 oldboy\]\# grep -n "." nginx.conf

1:stu01

2:stu02

3:stu03

4:stu04

5:stu05

6:stu06

7:stu07

8:stu08

9:stu09

10:stu10

11:stu11

12:stu12

13:stu13

14:stu14

15:stu15

16:stu16

17:stu17

18:stu18

19:stu19

20:stu20

#### awk

\[root@oldboy logs\]\# awk '{print NR,$0}' nginx.conf

1 stu01

2 stu02

3 stu03

4 stu04

5 stu05

6 stu06

7 stu07

8 stu08

9 stu09

10 stu10

11 stu11

12 stu12

13 stu13

14 stu14

15 stu15

16 stu16

17 stu17

18 stu18

19 stu19

20 stu20

#### sed

\[root@oldboy36 oldboy\]\# sed = nginx.conf \|xargs -n2

1 stu01

2 stu02

3 stu03

4 stu04

5 stu05

6 stu06

7 stu07

8 stu08

9 stu09

10 stu10

11 stu11

12 stu12

13 stu13

14 stu14

15 stu15

16 stu16

17 stu17

18 stu18

19 stu19

20 stu20

\[root@oldboy36 oldboy\]\# sed = nginx.conf \| sed 'N;s\#\n\# \#'

1 stu01

2 stu02

3 stu03

4 stu04

5 stu05

6 stu06

7 stu07

8 stu08

9 stu09

10 stu10

11 stu11

12 stu12

13 stu13

14 stu14

15 stu15

16 stu16

17 stu17

18 stu18

19 stu19

20 stu20

