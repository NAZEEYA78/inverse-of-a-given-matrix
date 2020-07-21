# inverse-of-a-given-matrix
makeVector <- function(x = numeric()) {
       m <- NULL
       set <- function(y) {
              x <<- y
              m <<- NULL
       }
       get <- function() x
       setmean <- function(mean) m <<- mean
       getmean <- function() m
       list(set = set, get = get,
            setmean = setmean,
            getmean = getmean)
}

cachemean <- function(x, ...) {
       m <- x$getmean()
       if(!is.null(m)) {
              message("getting cached data")
              return(m)
       }
       data <- x$get()
       m <- mean(data, ...)
       x$setmean(m)
       m
}
x1 <- makeInverse(matrix(c(1,2,3,4),2,2))
x1$getsolve() #Inverse not computed yet

cachesolve(x1) 

x1$set(x1$getsolve()) #Setting the function call to be the computed inverse
cachesolve(x1) #Inverse of the inverse is the original matrix
