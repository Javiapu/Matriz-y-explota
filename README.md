# Matriz-y-explota
Autolisp compatible con Autocad LT. Dibuja una matriz de camino con selección de distancia y luego explota la matriz. Tiene un pequeño error y aunque traté de desactivar el eco no funcionó bien nunca por lo que hay que pulsar un enter extra entre la ejecución de la matriz y la selección de la matriz para explotarla
(defun c:matyexp (/ sel path dist)   ; Function to create and explode path array
  (if (and (setq sel (ssget))
           (setq path (car (entsel "\nSelect path:")))
           (setq dist (cond ((getdist "\nEnter the Distance Between Objects <5>: "))
                           (5.)))
           (initcommandversion)
      )
    (progn    
      ; Create the array
      (command "._arraypath" sel "" path "" dist "")  
      ; Exit edit mode with "S" for "Salir"
      (command "S" "")
      ; Now try to explode
      (prompt "\nSeleccione la matriz para explotar: ")
      (command "._explode" pause)
    )
  )
  (princ)
)
