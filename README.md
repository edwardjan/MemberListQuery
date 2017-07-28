package DBM;

public class MemberListQuery
{
    
    public String getMemberListDateQuery(String ID)
    {
        String query = "SELECT DISTINCT t.date\n" +
        "FROM fos_user u\n" +
        "JOIN dts_timesheet t\n" +
        "ON u.id=t.user_id\n" +
        "JOIN pworeg_project_member p\n" +
        "ON u.id=p.member_id\n" +
        "JOIN pworeg_project w\n" +
        "ON p.proj_id=w.id\n" +
        "WHERE w.id=" + ID + "\n" +
        "ORDER BY t.date;";
        return query;
    }
    
    public String getMemberListNameQuery(String ID, String DateFrom, String DateTo)
    {
        String query = "SELECT DISTINCT concat(u.givenname, \" \", u.surname)\n" +
        "FROM pworeg_project p\n" +
        "JOIN pworeg_project_member pm\n" +
        "ON p.id=pm.proj_id\n" +
        "JOIN fos_user u\n" +
        "ON pm.member_id=u.id\n" +
        "JOIN dts_timesheet ts\n" +
        "ON u.id=ts.user_id\n" +
        "JOIN dts_project_timesheet_status ptsstat\n" +
        "ON ts.id=ptsstat.dtstimesheet_id\n" +
        "\n" +
        "WHERE p.id=" + ID + "\n" +
        "AND (ts.date>='" + DateFrom + "' AND ts.date<='" + DateTo + "')\n" +
        "ORDER BY ts.date;";
        return query;
    }
    
    public String getMemberListDatePeriodQuery(String ID, String DateFrom, String DateTo)
    {
        String query = "SELECT DISTINCT ts.date\n" +
        "FROM pworeg_project p\n" +
        "JOIN pworeg_project_member pm\n" +
        "ON p.id=pm.proj_id\n" +
        "JOIN fos_user u\n" +
        "ON pm.member_id=u.id\n" +
        "JOIN dts_timesheet ts\n" +
        "ON u.id=ts.user_id\n" +
        "JOIN dts_project_timesheet_status ptsstat\n" +
        "ON ts.id=ptsstat.dtstimesheet_id\n" +
        "\n" +
        "WHERE p.id=" + ID + "\n" +
        "AND (ts.date>='" + DateFrom + "' AND ts.date<='" + DateTo + "')\n" +
        "ORDER BY ts.date;";
        return query;
    }
    
    public String getMemberListHoursQuery(String ID, String Name, String Date)
    {
        String query = "SELECT COALESCE(NULLIF(ts.dailyHours,''), 'No Data')\n" +
        "FROM pworeg_project p\n" +
        "JOIN pworeg_project_member pm\n" +
        "ON p.id=pm.proj_id\n" +
        "JOIN fos_user u\n" +
        "ON pm.member_id=u.id\n" +
        "JOIN dts_timesheet ts\n" +
        "ON u.id=ts.user_id\n" +
        "JOIN dts_project_timesheet_status ptsstat\n" +
        "ON ts.id=ptsstat.dtstimesheet_id\n" +
        "WHERE p.id=" + ID + "\n" +
        "AND concat(u.givenname, \" \", u.surname)='" + Name + "'\n" +
        "AND ts.date='" + Date + "'\n" +
        "ORDER BY ts.date;";
        return query;
    }
    
}
