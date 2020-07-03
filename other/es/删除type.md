
POST edemo/test/_delete_by_query?conflicts=proceed
{
  "query": {
    "match_all": {}
  }
}