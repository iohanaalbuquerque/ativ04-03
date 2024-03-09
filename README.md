import sqlite3


def criar():
    conn = sqlite3.connect(‘filmes.db')
    cursor = conn.cursor()

cursor.execute("""
        CREATE TABLE IF NOT EXISTS filmes(
            id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
            nome VARCHAR(200) NOT NULL,
           genero VARCHAR(70) NOT NULL,
            classificação indicativa REAL NOT NULL);
    """)

 conn.close()


def novo_filme(nome, genero, classificação indicativa):
    conn = sqlite3.connect('filme.db')
    cursor = conn.cursor()

cursor.execute("""
        INSERT INTO filme(nome, genero, classificação indicativa )
        VALUES(?, ?, ?);
    """, (nome, genero, classificação indicativa))
    conn.commit()
    conn.close()


def listar_filme():
    conn = sqlite3.connect('filmes.db')
    cursor = conn.cursor()
    values = cursor.execute("SELECT * FROM filme")
    resultado = []
    for row in values:
        resultado.append({
            'id': row[0],
            'nome': row[1],
            'genero': row[2],
            'classificação indicativa’: row[3],
        })
    conn.close()
    return resultado


def atualiza_filme(id, nome, classificação indicativa):
    conn = sqlite3.connect('filmes.db')
    cursor = conn.cursor()
    cursor.execute(
        """
        UPDATE filmes
        SET nome=?, genero=?, classificação indicativa=?
        WHERE id=?;
        """,
        (nome, genero, classificação indicativa, id)
    )
    conn.commit()
    conn.close()


def remove_filme(id):
    conn = sqlite3.connect('filmes.db')
    cursor = conn.cursor()
    cursor.execute(
        """
        DELETE FROM filmes
        WHERE id=?;
        """,
        (id,)
    )
    conn.commit()
    conn.close()



def detalha_filme(id):
    conn = sqlite3.connect(‘filmes.db')
    cursor = conn.cursor()
    cursor.execute(
        """
        SELECT *
        FROM filmes
        WHERE id=?;
        """,
        (id,)
    )
    item = cursor.fetchone()
    conn.close()
    if item is None:
        return None
    return {
        'id': item[0],
        'nome': item[1],
        'genero': item[2],
        'classificação indicativa': item[3],
    }


if __name__=='__main__':
    criar()
