# tecintenet_escola_eduardo
Banco de dados exercicío

## Fazendo CRUD 
```sql
INSERT INTO cursos(titulo,CargaHoraria) 
VALUES(
    'Front-End',
    40
),
(
    'Back-End',
    80
),(
    'UX,UI Design',
    30
),(
    'Figma',
    10
),(
    'Redes de computadores',
    100
);

INSERT INTO professores(nome,AreaAtuacao,Cursos_id )
VALUES(
    'Jon oliva',
    'área infra',
    5
), (
    'Lemmy kilmister',
    'área Design',
    4
),(
    'Neil peart',
    'área Design',
    3
),(
    'Ozzy osbourne',
    'área desenvolvimento',
    2
),(
    'David gilmour',
    'área desenvolvimento',
    1
);

INSERT INTO alunos(nome,DataNascimento,PrimeiraNota,SegundaNota,Cursos_id)
VALUES
  ('Alex', '2000-03-21', 9.00, 7.00, 1),
    ('Ben', '2001-05-15', 8.50, 9.00, 2),
    ('Cathy', '1999-11-03', 7.20, 8.00, 3),
    ('David', '2002-02-08', 6.80, 6.50, 4),
    ('Eva', '2003-07-20', 9.50, 9.80, 5),
    ('Frank', '2000-12-10', 8.00, 7.50, 1),
    ('Grace', '2001-09-25', 7.70, 8.70, 2),
    ('Helen', '1998-04-14', 6.00, 5.50, 3),
    ('Ivan', '2002-08-30', 9.20, 9.40, 4);



```