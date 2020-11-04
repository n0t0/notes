### sed

grep -rl -- --DB_PASSWORD-- * | xargs -I@ sed -i ''  's/--DB_PASSWORD--/MT_CONPOOL_USER/g' @