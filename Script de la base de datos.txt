-- Crear la base de datos
CREATE DATABASE plataforma_empleos;
USE plataforma_empleos;

-- Tabla Candidatos
CREATE TABLE Candidatos (
    id_candidato INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellido VARCHAR(100) NOT NULL,
    correo VARCHAR(100) UNIQUE NOT NULL,
    contrasena VARCHAR(255) NOT NULL,
    telefono VARCHAR(20),
    direccion VARCHAR(255),
    ciudad_provincia VARCHAR(100),
    fecha_registro DATE
);

-- Tabla Empresas
CREATE TABLE Empresas (
    id_empresa INT AUTO_INCREMENT PRIMARY KEY,
    nombre_empresa VARCHAR(100) NOT NULL,
    correo VARCHAR(100) UNIQUE NOT NULL,
    contrasena VARCHAR(255) NOT NULL,
    direccion VARCHAR(255),
    telefono VARCHAR(20),
    fecha_registro DATE
);

-- Tabla Ofertas
CREATE TABLE Ofertas (
    id_oferta INT AUTO_INCREMENT PRIMARY KEY,
    id_empresa INT,
    titulo_puesto VARCHAR(100) NOT NULL,
    descripcion TEXT,
    requisitos TEXT,
    fecha_publicacion DATE,
    FOREIGN KEY (id_empresa) REFERENCES Empresas(id_empresa)
);

-- Tabla Aplicaciones
CREATE TABLE Aplicaciones (
    id_aplicacion INT AUTO_INCREMENT PRIMARY KEY,
    id_oferta INT,
    id_candidato INT,
    fecha_aplicacion TIME,
    FOREIGN KEY (id_oferta) REFERENCES Ofertas(id_oferta),
    FOREIGN KEY (id_candidato) REFERENCES Candidatos(id_candidato)
);

-- Tabla Habilidades
CREATE TABLE Habilidades (
    id_habilidad INT AUTO_INCREMENT PRIMARY KEY,
    id_candidato INT,
    habilidad VARCHAR(45),
    FOREIGN KEY (id_candidato) REFERENCES Candidatos(id_candidato)
);

-- Tabla Idiomas
CREATE TABLE Idiomas (
    id_idiomas INT AUTO_INCREMENT PRIMARY KEY,
    id_candidato INT,
    idioma VARCHAR(45),
    nivel VARCHAR(45),
    FOREIGN KEY (id_candidato) REFERENCES Candidatos(id_candidato)
);

-- Tabla CV
CREATE TABLE CV (
    id_cv INT AUTO_INCREMENT PRIMARY KEY,
    id_candidato INT,
    objetivo_profesional TEXT,
    logros_proyectos TEXT,
    disponibilidad VARCHAR(50),
    redes_sociales VARCHAR(255),
    foto VARCHAR(255),
    cv_pdf VARCHAR(255),
    fecha_creacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (id_candidato) REFERENCES Candidatos(id_candidato)
);

-- Tabla Formaciones
CREATE TABLE Formaciones (
    id_formacion INT AUTO_INCREMENT PRIMARY KEY,
    id_candidato INT,
    institucion VARCHAR(150),
    titulo VARCHAR(150),
    fecha_inicio DATE,
    fecha_fin DATE,
    FOREIGN KEY (id_candidato) REFERENCES Candidatos(id_candidato)
);

-- Tabla Experiencias
CREATE TABLE Experiencias (
    id_experiencia INT AUTO_INCREMENT PRIMARY KEY,
    id_candidato INT,
    empresa VARCHAR(150),
    puesto VARCHAR(150),
    descripcion TEXT,
    fecha_inicio DATE,
    fecha_fin DATE,
    FOREIGN KEY (id_candidato) REFERENCES Candidatos(id_candidato)
);

-- Tabla Referencias
CREATE TABLE Referencias (
    id_referencia INT AUTO_INCREMENT PRIMARY KEY,
    id_candidato INT,
    nombre_contacto VARCHAR(100),
    empresa_contacto VARCHAR(100),
    telefono_contacto VARCHAR(20),
    correo_contacto VARCHAR(100),
    FOREIGN KEY (id_candidato) REFERENCES Candidatos(id_candidato)
);
