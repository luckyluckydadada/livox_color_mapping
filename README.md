# livox_color_mapping
核心： scanRegistration 和 laserMapping

对于非彩色建图:
PointXYZI{
    float x,y,z;
    float intensity;
}
使用pcl::PointXYZI表示点云中的点，但是建图没有用intensity，只用了xyz，但是使用了intensity的存储空间做别的事情，详见laserMapping.cpp

对于彩色建图
使用pcl::PointXYZRGBNormal结构体代替自定义的PointXYZRGBI，pcl没有PointXYZRGBI结构体，自定义的PointXYZRGBI结构体不含很过内置函数，使用pcl::PointXYZRGBNormal也是无奈之举。
ros的消息为xyzi，因此fromROSMsg报错Failed to find match for field 'curvature'不用理会，其实我们也只使用xyz建图，使用了curvature的存储空间做别的事情。
PointXYZRGBNormal{
    float x,y,z;
    uint_8 r,g,b;
    float curvature;
    float normal_x，normal_y，normal_z;
}